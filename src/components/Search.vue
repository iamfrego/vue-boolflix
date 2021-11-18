<template>
  <div class="search">
    <input type="text" placeholder="Inserisci Titolo" v-model="title" />
    <button @click="titleSearch">Search</button>
    <ul>
      <li v-for="film in films" :key="film.id">
        <p>{{ film.title }}</p>
        <p>{{ film.original_title }}</p>
        <p></p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      films: [],
      error: "",
      title: "",
      API: "https://api.themoviedb.org/3/search/movie?api_key=2098b5dfde8029414f02b0a439961147&query=Ritorno",
    };
  },
  mounted() {
    axios.get(this.API).then((r) => {
      this.films = r.data.results;
      console.log(this.films);
    });
  },
  methods: {
    titleSearch() {},
  },
};
</script>

<style>
</style>