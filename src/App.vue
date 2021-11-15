<template>
  <div id="app">
    <SiteHeader />
    <SiteMain />
    <SiteFooter />
  </div>
</template>

<script>
import axios from "axios";
import SiteHeader from "./components/SiteHeader.vue";
import SiteMain from "./components/SiteMain.vue";
import SiteFooter from "./components/SiteFooter.vue";
export default {
  name: "App",
  components: {
    SiteHeader,
    SiteMain,
    SiteFooter,
  },
  mounted() {
    axios
      .get("https://flynn.boolean.careers/exercises/api/array/music")
      .then((r) => {
        console.log(r);
      })
      .catch((e) => {
        console.log(e, "Non funge");
      });
  },
};
</script>

<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap.scss";
</style>
