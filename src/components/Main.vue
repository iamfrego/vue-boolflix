<template>
  <div class="main">
    <Search @search-film="titleSearch" />
    <h1>Film</h1>
    <ul>
      <li v-for="film in films" :key="film.id">
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
    <h1>Serie TV</h1>
    <ul>
      <li v-for="serie in series" :key="serie.id">
        <p>{{ serie.name }}</p>
        <p>{{ serie.original_name }}</p>
        <div class="language">
          <span v-if="serie.original_language == 'en'">
            <flag iso="us" />
          </span>
          <span v-else-if="serie.original_language == 'ja'">
            <flag iso="jp" />
          </span>
          <span v-else-if="serie.original_language == 'zh'">
            <flag iso="cn" />
          </span>
          <span v-else>
            <flag :iso="serie.original_language" />
          </span>
        </div>
        <span> {{ serie.original_language }}</span>
        <p>{{ serie.vote_average }}</p>
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

  methods: {
    titleSearch(films) {
      this.title = films;

      var movie = `https://api.themoviedb.org/3/search/movie?api_key=2098b5dfde8029414f02b0a439961147&query=${this.title}`;

      var series = `https://api.themoviedb.org/3/search/tv?api_key=2098b5dfde8029414f02b0a439961147&query=${this.title}`;

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