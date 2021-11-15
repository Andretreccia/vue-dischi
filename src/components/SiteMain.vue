<template>
  <main>
    <p>main</p>
  </main>
</template>

<script>
import axios from "axios";
export default {
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
</style>