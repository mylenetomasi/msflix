<template>
  <div class="movie-detail">
    <div class="parte1">
      <h2>{{ movie.Title }}</h2>
      <p>{{ movie.Year }}</p>
      <p>{{ movie.Plot }}</p>
    </div>
    <div class="parte2">
      <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    </div>
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
    return {
      movie,
    };
  },
};
</script>
<style lang="scss" scoped>
.movie-detail {
  padding: 16px;
  display: flex;
  flex-direction: row;
  h2 {
    color: black;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }
  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }
  p {
    color: black;
    font-size: 18px;
    line-height: 1.4;
  }
}
.featured-img {
  display: block;
  max-width: 300px;
  margin-bottom: 16px;
}
.parte1 {
  width: 700px;
}
.parte2 {
  margin-left: 30px;
}
</style>
