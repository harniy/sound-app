<template>
  <div class="container">
    <h3>Fire</h3>
    <div class="fire_section section">
      <div
        class="fire"
        v-for="(fire, idx) in fires"
        :key="idx"
        @click="fireSound(fire.sound, idx)"
        :class="{active: idx === isActive}"
      >
        <img :src="fire.img" />
        <p class="fire_description">{{ fire.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fires: [
        {
          img: require("../assets/icons/fire.png"),
          sound: require("../assets/sounds/fire/fire.mp3"),
          description: "Fire",
        },
        {
          img: require("../assets/icons/bonfire.png"),
          sound: require("../assets/sounds/fire/bonfire.mp3"),
          description: "Bonfire",
        },
        {
          img: require("../assets/icons/campfire.png"),
          sound: require("../assets/sounds/fire/campfire.mp3"),
          description: "Campfire",
        },
      ],
      isActive: null,
      play: true,
      firePlay: "",
    };
  },
  methods: {
    fireSound(sound, i) {

        if (this.firePlay != "") {
        this.firePlay.pause();
      }
      this.firePlay = new Audio(sound);
      this.firePlay.play();

      this.firePlay.dataset.name = this.fires[i].description;
      this.firePlay.loop = true;

      this.isActive = i;
        this.setFire()
    },
    setFire(){
        this.$emit('setFire', this.firePlay )
    }
  },
};
</script>



<style>
</style>