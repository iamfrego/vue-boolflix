<template>
  <div class="main">
    <div class="search-box d-flex justify-content-sm-end">
      <Search @search-film="titleSearch" />
    </div>
    <!-- ./SEARCH -->
    <h1 class="text-white mb-5">Film</h1>
    <div
      class="
        row-cols-xxl-5 row-cols-xl-4 row-cols-lg-3 row-cols-md-2 row row-cols-1
      "
    >
      <div class="col mb-5" v-for="film in films" :key="film.id">
        <div class="img_wrap text-center">
          <img
            v-if="film.poster_path !== null"
            :src="'https://image.tmdb.org/t/p/w342' + film.poster_path"
            :alt="film.title"
          />
          <img v-else src="https://http.cat/206" alt="" class="img-fluid" />
        </div>
        <!-- ./IMAGE OF FILM -->
        <div class="title-box text-white p-6">
          <h3>Titolo: {{ film.title }}</h3>
          <p>Titolo originale: {{ film.original_title }}</p>
        </div>
        <!-- ./TITLE BOX -->
        <div class="language-box">
          <div class="language text-center">
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
          <div class="text-white text-center">
            {{ film.original_language }}
          </div>
        </div>
        <!-- ./LANGUAGE -->
        <div class="vote text-center">
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
        <!-- ./VOTE -->
      </div>
    </div>

    <h1 class="text-white mb-5">Serie TV</h1>
    <div class="row row-cols-5">
      <div class="col mb-5" v-for="serie in series" :key="serie.id">
        <div class="img_wrap text-center">
          <img
            v-if="serie.poster_path !== null"
            :src="'https://image.tmdb.org/t/p/w342' + serie.poster_path"
            :alt="serie.name"
          />
          <img v-else src="https://http.cat/206" alt="" class="img-fluid" />
        </div>
        <!-- ./IMAGE OF serie -->
        <div class="title-box text-white p-6">
          <h3>Titolo: {{ serie.name }}</h3>
          <p>Titolo originale: {{ serie.original_name }}</p>
        </div>
        <!-- ./TITLE BOX -->
        <div class="language-box">
          <div class="language text-center">
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
          <div class="text-white text-center">
            {{ serie.original_language }}
          </div>
        </div>
        <!-- ./LANGUAGE -->
        <div class="vote text-center">
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
        <!-- ./VOTE -->
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
.p-6 {
  padding-left: 24px;
}
.main {
  margin-top: 100px;
}

.active_star {
  color: yellow;
}
</style>