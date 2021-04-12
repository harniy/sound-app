<template>
  <div class="container">
    <h3>Rain</h3>
    <div class="rain_section section">
      <div
        class="rain"
        v-for="(rain, idx) in rains"
        :key="idx"
        @click="rainSound(rain.sound, idx)"
        :class="{ active: idx === isActive }"
      >
        <img :src="rain.img" />
        <p class="fire_description">{{ rain.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rains: [
        {
          img: require("../assets/icons/light_rain.png"),
          sound: require("../assets/sounds/rain/light_rain.mp3"),
          description: "Light",
        },
        {
          img: require("../assets/icons/spring_rain.png"),
          sound: require("../assets/sounds/rain/spring_rain.mp3"),
          description: "Spring",
        },
        {
          img: require("../assets/icons/heavy_rain.png"),
          sound: require("../assets/sounds/rain/heavy_rain.mp3"),
          description: "Heavy",
        },
        {
          img: require("../assets/icons/roof_rain.png"),
          sound: require("../assets/sounds/rain/roof_rain.mp3"),
          description: "Roof",
        },
        {
          img: require("../assets/icons/umbrella_rain.png"),
          sound: require("../assets/sounds/rain/umbrella_rain.mp3"),
          description: "Umbrella",
        },
        {
          img: require("../assets/icons/forest_rain.png"),
          sound: require("../assets/sounds/rain/forest_rain.mp3"),
          description: "Forest",
        },
        {
          img: require("../assets/icons/car_rain.png"),
          sound: require("../assets/sounds/rain/car_rain.mp3"),
          description: "Car",
        },
        {
          img: require("../assets/icons/car_rain2.png"),
          sound: require("../assets/sounds/rain/car_rain2.mp3"),
          description: "Car",
        },
      ],
      isActive: null,
      play: true,
      rainPlay: "",
    };
  },
  methods: {
    rainSound(sound, i) {
      if (this.rainPlay != "") {
        this.rainPlay.pause();
      }
      this.rainPlay = new Audio(sound);
      this.rainPlay.play();

      this.rainPlay.dataset.name = this.rains[i].description;
      this.rainPlay.loop = true;

      this.isActive = i;

      this.setRain()
    },
     setRain(){
        this.$emit('setRain', this.rainPlay )
    } 
  },
};
</script>

<style>
</style>