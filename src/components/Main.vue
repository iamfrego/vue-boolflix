<template>
  <div class="main">
    <Search @search-film="titleSearch" />
    <ul>
      <li v-for="film in films" :key="film.id">
        <p>{{ film.title }}</p>
        <p>{{ film.original_title }}</p>

        <div class="language">
          <span>Lingua: </span>
          <span v-if="film.original_language == 'en'">
            <flag iso="gb" />
          </span>
          <span v-else-if="film.original_language == 'zh'">
            <flag iso="cn" />
          </span>
          <span v-else-if="film.original_language == 'ja'">
            <flag iso="jp" />
          </span>
          <span v-else>
            {{ film.original_language }}
          </span>
        </div>

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
      flag: "riginal_language",
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