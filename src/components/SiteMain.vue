<template>
  <main id="site-main">
    <div class="container">
      <div class="row">
        <div class="card" v-for="music in musics" :key="music.ident"></div>
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
}
</style>