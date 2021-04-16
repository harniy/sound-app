<template>
  <div class="container">
    <h3>Lighting</h3>
    <div class="lighting_section section">
      <div
        class="lighting"
        v-for="(lighting, idx) in lightings"
        :key="idx"
        @click="lightingSound(lighting.sound, idx)"
        :class="{ active: idx === isActive }"
      >
        <img :src="lighting.img" />
        <p class="description">{{ lighting.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      lightings: [
        {
          img: require("../assets/icons/light.png"),
          sound: require("../assets/sounds/lighting/light.mp3"),
          description: "Light",
        },
        {
          img: require("../assets/icons/summer.png"),
          sound: require("../assets/sounds/lighting/summer.mp3"),
          description: "Summer",
        },
        {
          img: require("../assets/icons/storm.png"),
          sound: require("../assets/sounds/lighting/storm.mp3"),
          description: "Storm",
        },
      ],
      isActive: null,
      lightingPlay: "",
    };
  },
  methods: {
    lightingSound(sound, i) {
      if (this.lightingPlay != "") {
        this.lightingPlay.pause();
      }
      this.lightingPlay = new Audio(sound);
      this.lightingPlay.play();

      this.lightingPlay.dataset.name = this.lightings[i].description;
      this.lightingPlay.loop = true;

      this.isActive = i;

      this.setLighting();
    },
    setLighting() {
      this.$emit("setLighting", this.lightingPlay);
    },
  },
};
</script>