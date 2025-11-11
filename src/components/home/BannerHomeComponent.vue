
<script setup>
import { ref, onMounted } from "vue";

const API_KEY = "5d8c190e6ed5b1f514046b8593c595e5";
const HORROR_GENRE_ID = 27;
const topMovie = ref(null);

async function getTopHorrorMovie() {
  const url = `https://api.themoviedb.org/3/discover/movie?api_key=${API_KEY}&language=pt-BR&with_genres=${HORROR_GENRE_ID}&sort_by=vote_average.desc&vote_count.gte=200`;
  const res = await fetch(url);
  const data = await res.json();
  topMovie.value = data.results[0]; // pega o melhor avaliado
}

onMounted(getTopHorrorMovie);
</script>

<template>
  <section
    class="banner"
    v-if="topMovie"
    :style="{
      backgroundImage: `url(https://image.tmdb.org/t/p/original${topMovie.backdrop_path})`,
    }"
  >
    <div class="overlay">
      <div class="avaliacao">
        <p>Avaliação dos usuários</p>
        <p class="avaliacao"> <i class="mdi mdi-star-check-outline"></i> {{ topMovie.vote_average.toFixed(1) }}%</p>
      </div>
      <div class="dados">
      <h1>{{ topMovie.title }}</h1>
      <p class="classificacao">
      {{ topMovie.adult ? "18+" : "Livre" }}
      </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.banner {
  position: relative;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 80vh;
  display: flex;
  align-items: flex-end;
  color: white;
}

.overlay {
  width: 100%;
  padding: 40px;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.85), transparent);
}

.overlay h1 {
  font-size: 40px;
  margin-bottom: 10px;
  color: #F81F3E;
}

.avaliacao {
  color: #F81F3E;
  font-size: 50px;
}

.classificacao {
  font-size: 30px;
  background-color: #F81F3E;
  border-radius: 10px;
  color: #000000;
}
</style>
