<template>
  <div class="main">
    <Search @search-film="titleSearch" />
    <ul>
      <li v-for="film in globalSearch" :key="film.id">
        <p>{{ film.title }}</p>
        <p>{{ film.original_title }}</p>
        <div class="language">
          <span v-if="film.original_language == 'en'">
            <flag iso="us" />
          </span>
          <span v-else-if="film.original_language == 'ja'">
            <flag iso="jp" />
          </span>
          <span v-else-if="film.original_language == 'zh'">
            <flag iso="cn" />
          </span>
          <span v-else>
            <flag :iso="film.original_language" />
          </span>
        </div>
        <span> {{ film.original_language }}</span>
        <p>{{ film.vote_average }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import Search from "./Search.vue";
import axios from "axios";

export default {
  components: {
    Search,
  },
  data() {
    return {
      films: [],
      series: [],
      title: "",
    };
  },

  computed: {
    globalSearch() {
      return [...this.films, ...this.series];
    },
  },
  methods: {
    titleSearch(films) {
      this.title = films;

      let movie = {
        method: "get",
        url: `https://api.themoviedb.org/3/search/movie?api_key=2098b5dfde8029414f02b0a439961147&query=${this.title}`,
      };

      let series = {
        method: "get",
        url: `https://api.themoviedb.org/3/tv/popular?api_key=2098b5dfde8029414f02b0a439961147&query=${this.title}`,
      };

      axios.get(movie).then((r) => {
        this.films = r.data.results;
        console.log(this.title);
      });

      axios.get(series).then((r) => {
        this.series = r.data.results;
        console.log(this.title);
      });
    },
  },
};
</script>

<style>
</style>