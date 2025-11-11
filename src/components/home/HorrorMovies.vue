
<script setup>
import { ref, onMounted } from "vue";

const API_KEY = "5d8c190e6ed5b1f514046b8593c595e5";
const HORROR_GENRE_ID = 27;
const movies = ref([]);

async function getHorrorMovies() {
  const url = `https://api.themoviedb.org/3/discover/movie?api_key=${API_KEY}&language=pt-BR&with_genres=${HORROR_GENRE_ID}`;
  const res = await fetch(url);
  const data = await res.json();
  movies.value = data.results;
}

onMounted(getHorrorMovies);
</script>

<template>
  <section class="p-6 bg-black text-white min-h-screen">
    <h1 class="text-3xl font-bold mb-4 text-red-500">🎬 Filmes de Terror</h1>

    <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
      <div
        v-for="movie in movies"
        :key="movie.id"
        class="bg-gray-900 p-2 rounded-2xl shadow-md hover:scale-105 transition"
      >
        <img
          v-if="movie.poster_path"
          :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
          :alt="movie.title"
          class="rounded-lg mb-2"
        />
        <h2 class="text-lg font-semibold">{{ movie.title }}</h2>
        <p class="text-sm opacity-70 line-clamp-3">{{ movie.overview }}</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
