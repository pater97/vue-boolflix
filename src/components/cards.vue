<template>
  <div class="card">
    <!-- copertina card  -->
    <section class="cover">
      <!-- se trovata -->
      <img
        class="cover_img"
        v-if="film.poster_path"
        :src="coverLink + film.poster_path"
        :alt="film.title"
      />
      <!-- immagine non trovata  -->
      <img
        class="cover_img"
        v-else
        src="https://i.pinimg.com/originals/fd/78/c4/fd78c47f2a009df65b5b5a46f4437399.png"
        :alt="film.title"
      />
    </section>
    <section class="info">
      <!-- titolo -->
      <div class="title">
        <h1 v-if="film.title">{{ film.title }}</h1>
        <h1 v-else>{{ film.name }}</h1>
      </div>
      <!-- titolo originale -->
      <div class="original_title">
        <h2
          v-if="
            film.original_title | (film.original_name == film.title) | film.name
          "
        >
          original title: {{ film.original_title | film.original_name }}
        </h2>
      </div>
      <!-- voto -->
      <div class="stars">
        <span
          class="vote"
          v-for="finalVote in Math.round(film.vote_average / 2)"
          :key="finalVote"
        >
          <img src="../assets/star-solid.svg" alt="" />
        </span>
      </div>
      <!-- sezione flag e language -->
      <div class="lenguage">
        <h5>lenguage: {{ film.original_language }}</h5>
        <!-- bandiere frequenti da convertire -->
        <country-flag
          v-if="film.original_language == 'en'"
          country="gb"
          size="normal"
        />
        <country-flag
          v-else-if="film.original_language == 'ja'"
          country="jp"
          size="normal"
        />
        <country-flag
          v-else-if="film.original_language == 'ko'"
          country="kr"
          size="normal"
        />
        <country-flag
          v-else-if="film.original_language == 'zh'"
          country="cn"
          size="normal"
        />
        <!-- bandiere presenti nella libreria -->
        <country-flag v-else :country="film.original_language" size="normal" />
      </div>
      <div class="overview">
        {{ film.overview }}
      </div>
      <!-- sezione per mostrare il cast  -->
      <!-- ancoraggio per richiamare la tab  -->
      <div class="more_info" @click="getTab(film.id)">
        <h5>SHOW CAST...</h5>
      </div>
      <!-- in caso di informazioni del cast positive  -->
      <div :class="{ hidden_cast: castTabNone, castClass: castTab }">
        <div v-if="cast.length > 0">
          <h1>CAST:</h1>
          <div class="cycleCast" v-for="item in cast" :key="item.name">
            <h5>{{ item.name }}</h5>
          </div>
        </div>
        <!-- se il cast non è disponibile  -->
        <div v-else>
          <span class="cast_not_found">Cast not avalabile</span>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import CountryFlag from "vue-country-flag";
import "@fontsource/antonio";
import axios from "axios";
export default {
  components: {
    CountryFlag,
  },
  props: {
    film: Object,
  },
  data() {
    return {
      coverLink: "http://image.tmdb.org/t/p/w342/",
      apiUrl: "https://api.themoviedb.org/3/movie/",
      apiKey: "/credits?api_key=f4f382566368553eb6b723d584f2ef40",
      castTab: false,
      castTabNone: true,
      cast: [],
    };
  },
  methods: {
    getCast(filmId) {
      axios
        .get(this.apiUrl + filmId + this.apiKey)
        .then((response) => {
          this.cast = [];
          for (let i = 0; i < 5; i++) {
            this.cast.push(response.data.cast[i]);
            console.log(this.cast);
          }
        })
        .catch((e) => {
          console.log(e, "ops!");
        });
    },
    getTab(filmID) {
      this.getCast(filmID);
      this.castTab = true;
      this.castTabNone = false;
    },
  },
};
</script>

<style lang="scss">
.card {
  width: 90%;
  height: 21rem;
  margin: auto;
  position: relative;
  color: white;
  font-family: "Antonio";
  border-radius: 5px;
  overflow-y: clip;
  &:hover {
    box-shadow: 0px 0px 12px 1px #e50914;
    transform: scale(105%);
  }
  &:hover .cover_img {
    filter: blur(5px) brightness(0.5);
  }
  &:hover .info {
    z-index: 11;
  }
  .cover {
    img {
      width: 100%;
      position: absolute;
      z-index: 10;
      height: 100%;
      object-fit: cover;
    }
  }
  .info {
    position: absolute;
    z-index: 9;
    display: flex;
    flex-direction: column;
    padding: 0.5rem;
    height: 100%;
    div {
      height: calc(100% / 6);
    }
    .title {
      font-size: 1.5rem;
    }
    .original_title {
      font-size: 0.8rem;
    }
    .stars {
      margin: 0.5rem 0;
    }
    .lenguage {
      display: flex;
      align-items: center;
    }
    .overview {
      height: 8rem;
      overflow-y: auto;
      margin: 0.5rem 0;
    }
    .more_info {
      h5 {
        color: red;
        &:hover {
          cursor: pointer;
        }
      }
    }
    .castClass {
      background: black;
      padding: 1rem;
      position: absolute;
      height: 100%;
      width: 100%;
      top: 0;
      left: 0;
      color: white;
      h1{
        color: red;
      }
    }
    .hidden_cast {
      display: none;
    }
    .cycleCast{
      padding: 1rem;
    }
    .cast_not_found{
      color: red;
    }
  }
}
.vote {
  img {
    width: 15px;
    filter: invert(1);
  }
}
</style>