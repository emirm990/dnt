<template>
  <div id="app" v-on:mousemove="updateCoordinates">
    <MyButton v-bind:coords="coords" />
  </div>
</template>

<script>
import MyButton from "./components/MyButton.vue";

export default {
  name: "app",
  components: {
    MyButton
  },
  data() {
    return {
      coords: {
        x: 0,
        y: 0
      }
    };
  },
  methods: {
    updateCoordinates: function(event) {
      this.coords.x = event.clientX;
      this.coords.y = event.clientY;
    }
  }
};
</script>

<style>
body {
  margin: 0;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
}
</style>
