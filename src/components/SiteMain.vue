<template>
  <main id="site-main">
    <div class="container">
      <div class="row">
        <div class="col col-2" v-for="music in musics" :key="music.ident">
          <div class="card p-3">
            <div class="image">
              <img class="img-fluid" :src="music.poster" alt="" />
            </div>
            <div class="title">
              <h4>{{ music.title }}</h4>
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
    </div>
  </main>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      musics: [],
    };
  },
  mounted() {
    axios
      .get("https://flynn.boolean.careers/exercises/api/array/music")
      .then((r) => {
        this.musics = r.data.response;
      })
      .catch((e) => {
        console.log(e, "Non funge");
      });
  },
};
</script>

<style lang="scss">
#site-main {
  background: #1e2d3b;
  .row {
    padding-top: 7rem;
    .col {
      margin-top: 1rem;
      .card {
        height: 320px;
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