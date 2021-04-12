<template>
  <div class="container">
    <h3>Nature</h3>
    <div class="nature_section section">
      <div
        class="nature"
        v-for="(nature, idx) in natures"
        :key="idx"
        @click="natureSound(nature.sound, idx)"
        :class="{ active: idx === isActive }"
      >
        <img :src="nature.img" />
        <p class="wave_description">{{ nature.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      natures: [
        {
          img: require("../assets/icons/birds.png"),
          sound: require("../assets/sounds/nature/birds.mp3"),
          description: "Birds",
        },
        {
          img: require("../assets/icons/nightingale.png"),
          sound: require("../assets/sounds/nature/nightingale.mp3"),
          description: "Nightingale",
        },
        {
          img: require("../assets/icons/forest_bird.png"),
          sound: require("../assets/sounds/nature/forest.mp3"),
          description: "Forest",
        },
        {
          img: require("../assets/icons/park.png"),
          sound: require("../assets/sounds/nature/park.mp3"),
          description: "Park",
        },
        {
          img: require("../assets/icons/garden.png"),
          sound: require("../assets/sounds/nature/garden.mp3"),
          description: "Garden",
        },
        {
          img: require("../assets/icons/frog.png"),
          sound: require("../assets/sounds/nature/frog.mp3"),
          description: "Frog",
        },
        {
          img: require("../assets/icons/cricket.png"),
          sound: require("../assets/sounds/nature/cricket.mp3"),
          description: "Cricket",
        },
        {
          img: require("../assets/icons/cicada.png"),
          sound: require("../assets/sounds/nature/cicada.wav"),
          description: "Cicada",
        },
        {
          img: require("../assets/icons/night.png"),
          sound: require("../assets/sounds/nature/night.mp3"),
          description: "Night bugs",
        },
      ],
      isActive: "",
      naturePlay: "",
      natureAllSounds: [],
      soundsPlay: []
    };
  },
  methods: {
    natureSound(sound, i) {


      document.querySelectorAll(".nature").forEach((elem, idx) => {
        if (idx === i) {
          elem.classList.toggle("active");
        }
      });

      this.addSound(sound)

      this.setNatureInfo()

    },
   
    addSound(element){
      this.soundsPlay.forEach(elem => {
        elem.pause()
      })


      if(this.natureAllSounds.includes(element)){
        let indx = this.natureAllSounds.indexOf(element)
        this.natureAllSounds.splice(indx, 1)
      } else {
        this.natureAllSounds.push(element)
      }

      if(this.natureAllSounds.length > 0){
        this.soundsPlay = []
        this.natureAllSounds.forEach(elem => {

          let sound = new Audio(elem)
          sound.loop = true
          sound.volume = .5

          this.soundsPlay.push(sound)
          

          sound.play()
        })
      }
    },
    setNatureInfo(){
      this.$emit('setNature', this.soundsPlay)
    }
  },
};
</script>