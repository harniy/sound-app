<template>
  <div id="app">
    <Sound  />

    <Color @setColor="bgColor" />
  </div>
</template>

<script>
import Sound from "./components/sound";
import Color from "./components/color";

export default {
  name: "App",
  components: {
    Sound,
    Color,
  },
  data() {
    return {
      colorBackground: "#ffeb3bc4",
    };
  },
  methods: {
    bgColor(data) {
      this.colorBackground = data;

      localStorage.setItem('background', this.colorBackground)
    },
  },
  watch: {
    colorBackground() {
      document.querySelector("body").style.background = this.colorBackground;

      let items = document.querySelectorAll(".description");

      if (
        this.colorBackground === "#b4e43fd1" ||
        this.colorBackground === "#d12039" ||
        this.colorBackground === "#fff"
      ) {
        items.forEach((elem) => {
          elem.style.color = "#313131";
        });
      } else {
        items.forEach(elem => elem.style.color = '#8b8b8b')
      }
    },
  },
  mounted(){
    if(localStorage.getItem('background')){
      this.colorBackground = localStorage.getItem('background')
    }

  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  background: #ffeb3bc4;
}
</style>
