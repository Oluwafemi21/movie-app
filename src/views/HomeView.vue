<template>
    <keep-alive>
        <section>
            <div class="relative">
                <img
                    class="object-cover w-full md:h-72"
                    src="@/assets/avatar.jpg"
                    alt="Avatar The Last Air Bender"
                />
                <div
                    class="absolute bg-black/60 p-3 bottom-0 w-full text-white md:hidden"
                >
                    <h3 class="mb-2 font-bold">Avatar</h3>
                    <p>
                        In a war-torn world of elemental magic, a young boy
                        reawakens to undertake a dangerous mystic quest to
                        fulfill his destiny as the Avatar, and bring peace to
                        the world.
                    </p>
                </div>
            </div>
            <div class="container mx-auto md:ml-auto p-4">
                <form
                    class="text-center md:text-left py-5"
                    @submit.prevent="SearchMovie"
                >
                    <input
                        type="text"
                        v-model="searchValue"
                        placeholder="What movie are you looking for ?"
                        class="rounded py-2 px-3 bg-slate-500/40 font-medium w-full lg:w-1/3 md:w-1/2 mr-2 mb-3 md:mb-0 text-white focus:ring-2 hover:ring-2 outline-none hover:ring-green-500 focus:ring-green-500"
                    />
                    <button
                        class="bg-green-600 hover:bg-green-500 rounded text-white p-2 min-w-[100px] font-medium uppercase"
                    >
                        Search
                    </button>
                </form>
                <p class="text-white text-3xl mb-4">
                    <span v-show="item_length"
                        >Search results for "{{ movie }}"</span
                    >
                </p>
                <preloader v-show="loading" />
                <movie-card :movies="movies" />
                <div class="text-center">
                    <button
                        v-show="item_length"
                        class="text-white hover:text-green-500 mt-6"
                        @click="GetMore"
                    >
                        Show More Results...
                    </button>
                </div>
            </div>
        </section>
    </keep-alive>
</template>

<script>
import axios from "axios";
import MovieCard from "@/components/MovieCard.vue";
import Preloader from "@/components/Preloader.vue";

const baseUrl = "https://www.omdbapi.com/?apikey=10d2a084";

export default {
    name: "HomeView",
    data() {
        return {
            movie: "",
            searchValue: "",
            baseUrl,
            movies: [],
            item_length: 0,
            current_page: 1,
            loading: false,
        };
    },
    components: { MovieCard, Preloader },
    methods: {
        async SearchMovie() {
            this.loading = true;
            try {
                this.movie = this.searchValue;
                let res = await axios.get(`${this.baseUrl}&s=${this.movie}`);
                this.movies = res.data.Search;
                this.item_length = this.movies.length;
                this.loading = false;
            } catch (error) {
                console.error(error);
            }
        },
        async GetMore() {
            try {
                let res = await axios.get(
                    `${this.baseUrl}&s=${this.searchValue}&page=${
                        this.current_page + 1
                    }`
                );
                this.movies = this.movies.concat(res.data.Search);
            } catch (error) {
                console.error(error);
            }
        },
    },
};
</script>
