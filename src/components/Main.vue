<template>
  <div class="main">
    <Search @search-film="titleSearch" />
    <ul>
      <li v-for="film in films" :key="film.id">
        <p>{{ film.title }}</p>
        <p>{{ film.original_title }}</p>
        <p>{{ film.original_language }}</p>
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
      title: "",
    };
  },
  mounted() {},
  methods: {
    titleSearch(films) {
      this.title = films;
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=2098b5dfde8029414f02b0a439961147&query=${this.title}`
        )
        .then((r) => {
          this.films = r.data.results;
          console.log(this.title);
        });
    },
  },
};
</script>

<style>
</style>