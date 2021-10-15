<template>
  <div class="home">
    <div class="feature-card relative">
      <router-link to="/movie/tt0409591">
        <img
          src="http://www.omdbapi.com/src/poster.jpg"
          alt="Blade Runner Poster"
          class="featured-img block w-full h-72 object-cover relative z-0"
        />
        <div class="detail absolute left-0 right-0 bottom-0 p-4">
          <h3 class="text-white mb-4">Blade Runner</h3>
          <p class="text-white">
            Lorem ipsum dolor sit, amet consectetur adipisicing elit. Magnam
            illum id voluptatibus.
          </p>
        </div></router-link
      >
    </div>
    <form
      @submit.prevent="SearchMovies()"
      class="search-box flex flex-col justify-center items-center p-4"
    >
      <input
        class="
          block
          border-none
          outline-none
          appearance-none
          w-full
          text-white
          bg-gray-500
          text-lg
          rounded-lg
          mb-4
          duration-300
          placeholder-white
          focus:shadow-xs
          py-4
          px-3
        "
        type="text"
        name=""
        id=""
        placeholder="What are you looking for"
        v-model="search"
      />
      <input
        class="
          search
          block
          w-full
          max-w-xs
          border-none
          outline-none
          appearance-none
          p-4
          rounded-lg
          text-white text-xl
          uppercase
          duration-300
          bg-green-400
          active:bg-green-600
        "
        type="submit"
        value="Search"
      />
    </form>

    <div class="movies-list flex flex-wrap mx-0 my-2">
      <div class="movie px-4 py-2" v-for="movie in movies" :key="movie.imdbID">
        <router-link
          :to="'/movie/' + movie.imdbID"
          class="movie-link flex flex-col h-full"
        >
          <div class="product-image relative block">
            <img
              :src="movie.Poster"
              alt="Movie Poster"
              class="block w-full h-72 object-cover"
            />
            <div
              class="
                type
                absolute
                px-2
                py-4
                bg-green-500
                text-white
                bottom-4
                left-0
                uppercase
              "
            >
              {{ movie.Type }}
            </div>
          </div>
          <div class="detail bg-gray-600 px-4 py-2 text-gray-50">
            <p class="y text-lg">{{ movie.Year }}</p>
            <h3 class="font-semibold text-xl">{{ movie.Title }}</h3>
            <p class="genre text-lg text-gray-100">{{ movie.Genre }}</p>
          </div></router-link
        >
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from "vue";
import env from "@/env.js";
export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    };

    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>

<style scoped>
.detail {
  z-index: 1;
  flex: 1 1 100%;
  border-radius: 0px 0px 8px 8px;
}

.input {
  background: none;
}

.movie {
  max-width: 50%;
  flex: 1 1 50%;
}
</style>
