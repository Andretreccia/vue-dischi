<template>
  <main id="site-main">
    <SelectElement
      @genreFilter="addGenreValue"
    /><!-- pippoprende il valore che abbiamo passato e memorizzarlo  -->
    <div class="container">
      <div class="row justify-content-center py-5" v-if="this.loading == true">
        <div
          class="col col-2"
          v-for="music in filteredArrayMusics"
          :key="music.ident"
        >
          <div class="card p-3">
            <div class="image">
              <img class="img-fluid" :src="music.poster" alt="" />
            </div>
            <div class="title">
              <h4 class="text-center text-white text-uppercase fs-5">
                {{ music.title }}
              </h4>
            </div>
            <div class="author">
              <span>{{ music.author }}</span>
            </div>
            <div class="year">
              <span> {{ music.year }}</span>
            </div>
          </div>
        </div>
      </div>
      <div class="loading" v-else>
        <h1 class="text-light text-center">CARICAMENTO..</h1>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
import SelectElement from "./SelectElement.vue";
export default {
  components: {
    SelectElement,
  },
  data() {
    return {
      musics: [],
      loading: false,
      valueSelected: "",
    };
  },
  mounted() {
    setTimeout(this.callMusicApi, 3000);
  },
  methods: {
    callMusicApi() {
      axios
        .get("https://flynn.boolean.careers/exercises/api/array/music")
        .then((r) => {
          this.musics = r.data.response;
          this.loading = true;
        })
        .catch((e) => {
          console.log(e, "Non funge");
        });
    },
    addGenreValue(genreValue) {
      /* pippo conserva il valore del mio select */
      //console.log(genreValue);
      this.valueSelected = genreValue;
    },
  },
  computed: {
    filteredArrayMusics() {
      if (this.valueSelected == "") {
        return this.musics;
      }

      const arrayMusicFiltered = this.musics.filter((music) => {
        return music.genre.includes(this.valueSelected);
      });
      return arrayMusicFiltered;
    },
  },
};
</script>

<style lang="scss">
#site-main {
  background: #1e2d3b;
  min-height: calc(100vh - 80px);
  .row {
    .col {
      .card {
        margin-top: 1rem;
        height: 320px;
        width: 180px;
        background: rgba(255, 255, 255, 0.088);
        text-align: center;
        .image {
          margin-bottom: 1rem;
        }
        .title {
          color: white;
        }
        .author,
        .year {
          color: gray;
        }
      }
    }
  }
}
</style>