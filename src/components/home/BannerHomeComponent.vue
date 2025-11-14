<script setup>
import { ref, onMounted } from "vue";

const API_KEY = "5d8c190e6ed5b1f514046b8593c595e5";
const HORROR_GENRE_ID = 27;

const topHorrorMovies = ref([]);
const currentIndex = ref(0);

async function getTopHorrorMovies() {
  const url = `https://api.themoviedb.org/3/discover/movie?api_key=${API_KEY}&language=pt-BR&with_genres=${HORROR_GENRE_ID}&sort_by=vote_average.desc&vote_count.gte=200`;

  const res = await fetch(url);
  const data = await res.json();

  topHorrorMovies.value = data.results.slice(0, 4); // 4 melhores
}

// Botões do carrossel
function nextSlide() {
  currentIndex.value =
    (currentIndex.value + 1) % topHorrorMovies.value.length;
}

function prevSlide() {
  currentIndex.value =
    (currentIndex.value - 1 + topHorrorMovies.value.length) %
    topHorrorMovies.value.length;
}

onMounted(getTopHorrorMovies);
</script>
<template>
  <section class="carousel-container">
    <!-- Slides -->
    <div class="carousel-track" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
      <div v-for="movie in topHorrorMovies" :key="movie.id" class="slide" :style="{
        backgroundImage: `
      background: linear-gradient(to bottom, #f81f4000 0%, #60000E 50%, #191919 100%) transparent,;
      url(https://image.tmdb.org/t/p/original${movie.backdrop_path})
    `
      }">
        <div class="overlay">
          <div class="avaliacao">
            <p>Avaliação dos usuários</p>
            <p class="avaliacao"> <i class="mdi mdi-star-check-outline"></i> <span>{{ movie.vote_average.toFixed(1) }}%
              </span></p>
          </div>
          <div class="detalhes">
            <h1>{{ movie.title }}</h1>
            <div class="classificacao">
              {{ movie.adult ? `18` : `L` }}
            </div>

          </div>
        </div>
      </div>
    </div>

    <!-- Botões -->
    <button class="btn prev" @click="prevSlide"><i class="mdi mdi-pan-left"></i></button>
    <button class="btn next" @click="nextSlide"><i class="mdi mdi-pan-right"></i></button>
  </section>
</template>

<style scoped>
.carousel-container {
  position: relative;
  width: 100%;
  height: 80vh;
  overflow: hidden;
  background-color: black;
  color: white;
}

/* Área deslizante */
.carousel-track {
  display: flex;
  width: 100%;
  height: 100%;
  transition: transform 0.7s ease;
}

/* Cada slide */
.slide {
  width: 100%;
  height: 100%;
  flex-shrink: 0;
  background-size: cover;
  background-position: center;
  position: relative;
}

/* Escurecer embaixo para texto aparecer */
.overlay {
  position: absolute;
  bottom: 50%;
  width: 100%;
  padding: 40px;
  display: flex;
  justify-content: space-between;

  & .avaliacao {
    display: flex;
    flex-direction: column;

    & p {
      font-size: 25px;
      color: #F81F3E;
    }

    & .avaliacao {
      display: flex;
      flex-direction: column;
      text-align: center;
      align-items: center;
      background-color: #191919;
      padding: 10px 45px;
      border-radius: 100px;
      font-size: 50px;
      color: #F81F3E;
    }

    & span {
      margin: -10px;
    }
  }

  & .detalhes {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0 10vw;

    & h1 {
      font-size: 40px;
      margin-bottom: 10px;
      color: #F81F3E;
      background-color: #19191977;
      padding: 5px 10px;
      border-radius: 10px;
    }


    & .classificacao {
      font-size: 30px;
      color: #191919;
      font-weight: bold;
      -webkit-text-stroke: 2px #000000;
      padding: 5px 20px;
      background: #F81F3E;
      border-radius: 10px;
    }
  }
}

/* Botões */
.btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  cursor: pointer;
  color: #F81F3E;
  font-size: 100px;
  transition: 0.3s;

}

.btn:hover {
  color: rgba(0, 0, 0, 0.8);
}

.prev {
  left: 20px;
}

.next {
  right: 20px;
}
</style>
