<template>
  <div class="main">
    <div class="search-box d-flex justify-content-sm-end">
      <Search @search-film="titleSearch" />
    </div>
    <h1 class="text-white">Film</h1>
    <div class="row row-cols-5">
      <div class="col" v-for="film in films" :key="film.id">
        <div class="img_wrap">
          <img
            v-if="film.poster_path !== null"
            :src="'https://image.tmdb.org/t/p/w342' + film.poster_path"
            :alt="film.name"
          />
          <img v-else src="https://http.cat/417" alt="" />
        </div>
        <p class="text-white">{{ film.title }}</p>
        <p class="text-white">{{ film.original_title }}</p>
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
        <span class="text-white"> {{ film.original_language }}</span>
        <div class="vote">
          <div v-if="parseInt((film.vote_average / 2).toFixed(0)) !== 0">
            <span
              v-for="n in parseInt((film.vote_average / 2).toFixed(0))"
              :key="n.index"
            >
              <i class="fa fa-star active_star"></i>
            </span>
            <span
              v-for="n in 5 - parseInt((film.vote_average / 2).toFixed(0))"
              :key="n.index"
            >
              <i class="far fa-star text-white"></i>
            </span>
          </div>
          <div v-else>
            <span v-for="n in 5" :key="n">
              <i class="far fa-star text-white"></i>
            </span>
          </div>
        </div>
      </div>
    </div>

    <h1 class="text-white">Serie TV</h1>
    <div class="row row-cols-5">
      <div class="col" v-for="serie in series" :key="serie.id">
        <div class="img_wrap">
          <img
            v-if="serie.poster_path !== null"
            :src="'https://image.tmdb.org/t/p/w342' + serie.poster_path"
            :alt="serie.name"
          />
          <img v-else src="https://http.cat/417" alt="" />
        </div>
        <p class="text-white">{{ serie.name }}</p>
        <p class="text-white">{{ serie.original_name }}</p>
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
        <span class="text-white"> {{ serie.original_language }}</span>
        <div class="vote">
          <div v-if="parseInt((serie.vote_average / 2).toFixed(0)) !== 0">
            <span
              v-for="n in parseInt((serie.vote_average / 2).toFixed(0))"
              :key="n.index"
            >
              <i class="fa fa-star active_star"></i>
            </span>
            <span
              v-for="n in 5 - parseInt((serie.vote_average / 2).toFixed(0))"
              :key="n.index"
            >
              <i class="far fa-star text-white"></i>
            </span>
          </div>
          <div v-else>
            <span v-for="n in 5" :key="n">
              <i class="far fa-star text-white"></i>
            </span>
          </div>
        </div>
      </div>
    </div>
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
      });

      axios.get(series).then((r) => {
        this.series = r.data.results;
      });
    },
  },
};
</script>

<style>
.search-box {
  position: fixed;
  top: 50px;
  right: 25px;
  left: 0;
  z-index: 1030;
}
.active_star {
  color: yellow;
}
</style>