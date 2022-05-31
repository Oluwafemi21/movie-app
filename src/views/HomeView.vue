<template>
  <div class="min-h-screen bg-slate-900">
    <header class="bg-slate-900 text-center py-3">
      <h1 class="text-4xl font-medium text-white">
        <span class="text-green-500">Vue</span>Movies
      </h1>
    </header>
    <div class="relative">
      <img
        class="object-contain w-full"
        src="@/assets/avatar.jpg"
        alt="Avatar The Last Air Bender"
      />
      <div class="absolute bg-black/60 p-3 bottom-0 w-full text-white">
        <h3 class="mb-2 font-bold">Avatar</h3>
        <p>
          The last airbender has woken up from a deep sleep of over 100years
          with the aim of maintaining balance to the four nations which is
          primarily his duty.
        </p>
      </div>
    </div>
    <div class="container mx-auto p-4">
      <form class="text-center px-3 py-5" @submit.prevent="SearchMovie">
        <input
          type="text"
          v-model="searchValue"
          placeholder="What movie are you looking for ?"
          class="
            rounded
            p-3
            bg-slate-500/40
            font-medium
            w-full
            mb-3
            text-white
            focus:ring-2
            hover:ring-2
            outline-none
            hover:ring-green-500
            focus:ring-green-500
          "
        />
        <button
          class="
            bg-green-600
            hover:bg-green-500
            rounded
            text-white
            p-2
            min-w-[130px]
            uppercase
            font-medium
          "
        >
          Search
        </button>
      </form>
      <ul
        class="grid gap-x-4 gap-y-8 grid-cols-2 md:grid-cols-3 lg:grid-cols-4"
      >
        <li v-for="movie in movies" :key="movie.imdbID" class="relative">
          <img
            class="h-64 w-full object-cover"
            :src="movie.Poster"
            :alt="movie.Title"
          />
          <h5
            class="
              bg-green-600
              uppercase
              text-white
              py-2
              px-4
              rounded-r
              absolute
              top-0
            "
          >
            {{ movie.Type }}
          </h5>
          <div class="bg-slate-600 rounded-b py-2 px-1">
            <span class="text-sm text-gray-400">{{ movie.Year }}</span>
            <p class="text-white font-medium">{{ movie.Title }}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import MovieCard from "@/components/MovieCard.vue";

const baseUrl = "http://www.omdbapi.com/?apikey=10d2a084";

export default {
  name: "HomeView",
  data() {
    return {
      searchValue: "",
      baseUrl,
      movies: [],
    };
  },
  methods: {
    async SearchMovie() {
      let res = await axios.get(`${this.baseUrl}&s=${this.searchValue}`);

      this.movies = res.data.Search;

      console.log(res.data);
    },
  },
  components: { MovieCard },
};
</script>

