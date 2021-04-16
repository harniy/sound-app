<template>
  <div class="container">
    <h3>Water</h3>
    <div class="wave_section section">
      <div
        class="wave"
        v-for="(wave, idx) in waves"
        :key="idx"
        @click="waveSound(wave.sound, idx)"
        :class="{ active: idx === isActive }"
      >
        <img :src="wave.img" />
        <p class="description">{{ wave.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      waves: [
        {
          img: require("../assets/icons/river.png"),
          sound: require("../assets/sounds/wave/river.wav"),
          description: "River",
        },
        {
          img: require("../assets/icons/wave.png"),
          sound: require("../assets/sounds/wave/wave.wav"),
          description: "Wave",
        },
        {
          img: require("../assets/icons/big_wave.png"),
          sound: require("../assets/sounds/wave/big_wave.wav"),
          description: "Big wave",
        },
        {
          img: require("../assets/icons/sea_wave.png"),
          sound: require("../assets/sounds/wave/sea_wave.wav"),
          description: "Sea",
        },
        {
          img: require("../assets/icons/oceane.png"),
          sound: require("../assets/sounds/wave/oceane.wav"),
          description: "Oceane",
        },
      ],
      isActive: null,
      wavePlay: "",
    };
  },
  methods: {
    waveSound(sound, i) {
      if (this.wavePlay != "") {
        this.wavePlay.pause();
      }
      this.wavePlay = new Audio(sound);
      this.wavePlay.play();

      this.wavePlay.dataset.name = this.waves[i].description;
      this.wavePlay.loop = true;

      this.isActive = i;

      this.setwave();
    },
    setwave() {
      this.$emit("setwave", this.wavePlay);
    },
  },
};
</script>