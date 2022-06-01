<template>
  <ul class="grid gap-x-4 gap-y-8 grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
    <li v-for="movie in movies" :key="movie.imdbID" class="relative">
      <img
        class="w-full h-64 md:h-96 object-cover"
        :src="movie.Poster"
        :alt="movie.Title"
      />
      <router-link :to="'/movie/' + movie.imdbID">
        <button
          class="
            absolute
            top-5
            right-5
            h-6
            w-6
            text-center
            rounded-full
            text-white
            bg-black
            hover:bg-white hover:text-black
          "
        >
          i
        </button>
      </router-link>
      <h5
        class="
          bg-green-600
          uppercase
          text-white
          py-2
          px-4
          rounded-r
          absolute
          bottom-20
        "
      >
        {{ movie.Type }}
      </h5>
      <div class="bg-slate-600 rounded-b p-2">
        <span class="text-sm text-gray-400">{{ movie.Year }} </span>
        <p class="text-white font-medium truncate">{{ movie.Title }}</p>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  name: "Movie Card",
  props: ["movies"],
};
</script>

<style>
</style>