<template>
  <section class="min-h-[90.5vh] bg-slate-900">
    <div class="relative">
      <img
        class="object-contain w-full"
        src="@/assets/avatar.jpg"
        alt="Avatar The Last Air Bender"
      />
      <div class="absolute bg-black/60 p-3 bottom-0 w-full text-white">
        <h3 class="mb-2 font-bold">Avatar</h3>
        <p>
          In a war-torn world of elemental magic, a young boy reawakens to
          undertake a dangerous mystic quest to fulfill his destiny as the
          Avatar, and bring peace to the world.
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
      <p class="text-white text-3xl mb-4">
        <span v-show="item_length"
          >Search {{ item_length }} results for "{{ searchValue }}"</span
        >
      </p>
      <movie-card :movies="movies" />
    </div>
  </section>
</template>

<script>
import axios from "axios";
import MovieCard from "@/components/MovieCard.vue";

const baseUrl = "https://www.omdbapi.com/?apikey=10d2a084";

export default {
  name: "HomeView",
  data() {
    return {
      searchValue: "",
      baseUrl,
      movies: [],
      item_length: 0,
    };
  },
  methods: {
    async SearchMovie() {
      try {
        let res = await axios.get(`${this.baseUrl}&s=${this.searchValue}`);
        this.movies = res.data.Search;
        this.item_length = this.movies.length;
      } catch (error) {
        console.log(error);
      }
    },
  },
  components: { MovieCard },
};
</script>

