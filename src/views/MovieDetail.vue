<template>
  <section>
    <div class="container mx-auto px-8 pt-9">
      <router-link to="/">
        <button
          class="bg-green-600 text-white py-1 px-3 rounded hover:bg-green-500"
        >
          Back
        </button>
      </router-link>

      <div v-show="!loading" class="flex flex-col md:flex-row gap-12 mt-5">
        <img :src="movieInfo.Poster" :alt="movieInfo.Title" />

        <article class="text-white">
          <h1 class="text-4xl mb-4">Title: {{ movieInfo.Title }}</h1>
          <p class="mb-4">
            <span class="underline">Genre:</span> {{ movieInfo.Genre }}
          </p>
          <p class="mb-4">
            <span class="underline">Casts:</span> {{ movieInfo.Actors }}
          </p>
          <p class="mb-4">
            <span class="underline">Released:</span> {{ movieInfo.Released }}
          </p>
          <p class="mb-4">
            <span class="underline">Duration:</span> {{ movieInfo.Runtime }}
          </p>
          <p class="mb-4">
            <span class="underline">Plot:</span> {{ movieInfo.Plot }}
          </p>
        </article>
      </div>
      <preloader v-show="loading" />
    </div>
  </section>
</template>

<script>
import axios from "axios";
import Preloader from "@/components/Preloader.vue";
const baseUrl = "https://www.omdbapi.com/?apikey=10d2a084";
export default {
  components: { Preloader },
  name: "MovieDetail",
  data() {
    return {
      baseUrl,
      movieInfo: [],
      loading: true,
    };
  },
  async mounted() {
    try {
      let res = await axios.get(`${this.baseUrl}&i=${this.$route.params.id}`);

      this.movieInfo = res.data;
      this.loading = false;
    } catch (error) {
      console.log(error);
    }
  },
  created() {
    this.loading = true;
  },
};
</script>