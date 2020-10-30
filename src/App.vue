<template>
  <div id="app">
    <Camera v-on:takePicture="getPicture" />
    <Photo />
  </div>
</template>

<script>
import Camera from "./components/camera";
import Photo from "./components/photo"
export default {
  name: "App",
  components: {
    Camera,
    Photo
  },
  methods: {
    getPicture() {
      const picture = document.querySelector("canvas")

      const ctx = picture.getContext("2d")
      ctx.imageSmoothingEnabled = true
      ctx.imageSmoothingQuality = "high"
      ctx.drawImage(document.querySelector("video"), 0, 0, picture.width, picture.height)
    },
  },
};
</script>

<style lang="scss">
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  padding: 0;
  margin: 0;
  border: 0;
}
</style>
