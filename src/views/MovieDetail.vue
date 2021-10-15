<template>
  <div class="movie-detail p-4">
    <h2 class="text-white font-semibold text-3xl mb-4">{{ movie.Title }}</h2>
    <p class="text-white text-lg">{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="" class="featured-img block max-w-xs mb-4" />
    <p class="text-white text-lg">{{ movie.Plot }}</p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data;
        });
    });
    return { movie };
  },
};
</script>

<style></style>
