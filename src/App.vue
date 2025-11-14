<script setup>
import HeaderComponent from './components/HeaderComponent.vue';
import FooterComponent from './components/FooterComponent.vue.vue';
//import horror from './components/home/HorrorMovies.vue';
import BannerHomeComponent from './components/home/BannerHomeComponent.vue';
</script>
<template>
  <header>
    <headerComponent />
  </header>
  <main>
    <!--<RouterView />-->
    <BannerHomeComponent />

    <!--<horror />-->
  </main>
  <footer>
    <FooterComponent />
  </footer>
</template>

<style scoped>

</style>
