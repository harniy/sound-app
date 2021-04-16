<template>
  <div class="container end">
    <h3>World</h3>

    <div class="world_section section">
      <div
        class="world"
        v-for="(world, index) in worlds"
        :key="index"
        @click="worldSound(world.sound, index)"
        :class="{ active: index === isActive }"
      >
        <img :src="world.img" />
        <p class="description">{{ world.description }}</p>
      </div>
    </div>
  </div>
</template>



<script>
export default {
  data() {
    return {
      worlds: [
        {
          img: require("../assets/icons/chimes.png"),
          sound: require("../assets/sounds/world/chimes.mp3"),
          description: "Chimes",
        },
        {
          img: require("../assets/icons/train.png"),
          sound: require("../assets/sounds/world/train.mp3"),
          description: "Train",
        },
        {
          img: require("../assets/icons/train2.png"),
          sound: require("../assets/sounds/world/train2.mp3"),
          description: "Train",
        },
        {
          img: require("../assets/icons/typewriter.png"),
          sound: require("../assets/sounds/world/typewriter.mp3"),
          description: "Typewriter",
        },
        {
          img: require("../assets/icons/cars.png"),
          sound: require("../assets/sounds/world/cars.mp3"),
          description: "Cars",
        },
        {
          img: require("../assets/icons/street.png"),
          sound: require("../assets/sounds/world/street.mp3"),
          description: "Street",
        },
      ],
      isActive: null,
      worldPlay: '',
    };
  },
  methods: {
    worldSound(sound, i) {
    if (this.worldPlay != "") {
        this.worldPlay.pause();
      } 

      

      this.worldPlay = new Audio(sound);
      this.worldPlay.play()

       this.worldPlay.dataset.name = this.worlds[i].description;
      this.worldPlay.loop = true;


      this.isActive = i;

      this.setWorldInfo()
    },
    setWorldInfo(){
        this.$emit('setWorld', this.worldPlay)
    }
  },
};
</script>