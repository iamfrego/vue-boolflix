<template>
  <div class="main">
    <div class="search-box d-flex justify-content-sm-end">
      <Search @search-film="titleSearch" />
    </div>
    <!-- ./SEARCH -->

    <!-- FILM  and SERIE TVW -->
    <div class="nav d-flex justify-content-between">
      <h1 class="text-white mb-5">Film e Serie TV</h1>
    </div>

    <div
      class="
        row-cols-xxl-5 row-cols-xl-4 row-cols-lg-3 row-cols-md-2 row row-cols-1
      "
    >
      <div class="col mb-5" v-for="film in globalSearch" :key="film.id">
        <div class="film_card">
          <div class="img_wrap text-center">
            <img
              v-if="film.poster_path !== null"
              :src="'https://image.tmdb.org/t/p/w342' + film.poster_path"
              :alt="film.title"
            />
            <img v-else src="https://http.cat/206" alt="" class="img-fluid" />
          </div>
          <!-- ./IMAGE OF film -->
          <div class="info_film h-100">
            <div
              class="title-box text-white p-6"
              v-if="
                film.title !== film.original_title ||
                film.name !== film.original_name
              "
            >
              <h3 class="text-center">{{ film.title || film.name }}</h3>
              <p>
                Titolo originale:
                {{ film.original_title || film.original_name }}
              </p>
            </div>
            <div class="title-box text-white p-6" v-else>
              <h3 class="text-center">Titolo: {{ film.title || film.name }}</h3>
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
            <div class="vote py-3 text-center">
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
              <div v-else class="text-white">
                <p>N/A</p>
              </div>
            </div>
            <!-- ./VOTE -->
            <div class="overview text-white">
              <div v-if="film.overview.length < 100" class="overview">
                {{ film.overview }}
              </div>
              <div v-else class="overview">
                {{ film.overview.substr(0, 100) + "..." }}
              </div>
            </div>
            <!-- /.overview  -->
          </div>
        </div>
      </div>
      <!-- /FILM -->
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

  computed: {
    globalSearch() {
      return [...this.films, ...this.series];
    },
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

.col {
  height: 512px;
}

.info_film {
  padding: 2rem;
  display: none;
}

.active_star {
  color: yellow;
}

.film_card:hover {
  border: #e50914 5px solid;
  height: 100%;
}

.film_card:hover .img_wrap {
  display: none;
}

.film_card:hover .info_film {
  display: block;
}
</style>