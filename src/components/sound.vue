<template>
  <main>
    <div
      class="control_modal"
      v-if="
        soundPlay ||
        firePlay ||
        rainPlay ||
        lightingPlay ||
        wavePlay ||
        worldPlay
      "
    >
    
      <img class="close" src="../assets/icons/close.png" alt="" @click="closePanel">
      <img class="show" src='../assets/icons/show.png' alt="" @click="showPanel">
    
      <h3 class="modal_title">Control Sound</h3>
      <div class="sound_list">
        <ul>
          <li class="sound_item" v-if="soundPlay">
            <span>{{ soundPlay.dataset.name }}</span>
            <input type="range" min="1" max="10" v-model="windVolume" />
            <img
              src="../assets/icons/sound_on.png"
              alt=""
              @click="stopWind"
              v-if="wind"
            />
            <img
              src="../assets/icons/sound_off.png"
              alt=""
              @click="playWind"
              v-if="!wind"
            />
          </li>

          <li class="sound_item" v-if="firePlay">
            <span>{{ firePlay.dataset.name }}</span>
            <input type="range" min="1" max="10" v-model="fireVolume" />
            <img
              src="../assets/icons/sound_on.png"
              alt=""
              @click="stopFire"
              v-if="fire"
            />
            <img
              src="../assets/icons/sound_off.png"
              alt=""
              @click="playFire"
              v-if="!fire"
            />
          </li>
          <li class="sound_item" v-if="rainPlay">
            <span>{{ rainPlay.dataset.name }}</span>
            <input type="range" min="1" max="10" v-model="rainVolume" />
            <img
              src="../assets/icons/sound_on.png"
              alt=""
              @click="stopRain"
              v-if="rain"
            />
            <img
              src="../assets/icons/sound_off.png"
              alt=""
              @click="playRain"
              v-if="!rain"
            />
          </li>
          <li class="sound_item" v-if="lightingPlay">
            <span>{{ lightingPlay.dataset.name }}</span>
            <input type="range" min="1" max="10" v-model="lightingVolume" />
            <img
              src="../assets/icons/sound_on.png"
              alt=""
              @click="stopLighting"
              v-if="lighting"
            />
            <img
              src="../assets/icons/sound_off.png"
              alt=""
              @click="playLighting"
              v-if="!lighting"
            />
          </li>
          <li class="sound_item" v-if="wavePlay">
            <span>{{ wavePlay.dataset.name }}</span>
            <input type="range" min="1" max="10" v-model="waveVolume" />
            <img
              src="../assets/icons/sound_on.png"
              alt=""
              @click="stopWave"
              v-if="wave"
            />
            <img
              src="../assets/icons/sound_off.png"
              alt=""
              @click="playWave"
              v-if="!wave"
            />
          </li>
          <li class="sound_item" v-if="worldPlay">
            <span>{{ worldPlay.dataset.name }}</span>
            <input type="range" min="1" max="10" v-model="worldVolume" />
            <img
              src="../assets/icons/sound_on.png"
              alt=""
              @click="stopWorld"
              v-if="world"
            />
            <img
              src="../assets/icons/sound_off.png"
              alt=""
              @click="playWorld"
              v-if="!world"
            />
          </li>
        </ul>

        <div class="stop_all">
          <p v-if="!stopAll">Stop all</p>
          <img
            src="../assets/icons/sound_on.png"
            @click="stopAllSounds"
            v-if="!stopAll"
          />
          <p v-if="stopAll">Play all</p>
          <img
            src="../assets/icons/sound_off.png"
            @click="playAllSounds"
            v-if="stopAll"
          />
        </div>
      </div>
    </div>

    <div class="app_title">
      <h1>sound</h1>
      <p class="title">Create your Mood</p>
      <hr />
    </div>
    <div class="app_section">
      <div class="container">
        <h3>Wind</h3>
        <div class="wind_section section">
          <div
            class="wind"
            :class="{ active: idx === isActive }"
            v-for="(wind, idx) in winds"
            :key="idx"
            @click="getSound(wind.sound, idx)"
          >
            <img :src="wind.img" />
            <p class="wind_description">{{ wind.description }}</p>
          </div>
        </div>
      </div>

      <Fire @setFire="getFire" />

      <Rain @setRain="getRain" />

      <Lighting @setLighting="getLighting" />

      <Water @setwave="getWave" />

      <Nature @setNature="getNature" />

      <World @setWorld="getWorld" />
    </div>
  </main>
</template>



<script>
import Fire from "../components/fire";
import Rain from "../components/rain";
import Lighting from "../components/lightning";
import Water from "../components/water";
import Nature from "../components/nature";
import World from "../components/world";

export default {
  components: { Fire, Rain, Lighting, Water, Nature, World },
  data() {
    return {
      winds: [
        {
          img: require("../assets/icons/wind.png"),
          sound: require("../assets/sounds/wind/light.mp3"),
          description: "Light",
        },
        {
          img: require("../assets/icons/strong_wind.png"),
          sound: require("../assets/sounds/wind/strong.mp3"),
          description: "Strong",
        },
        {
          img: require("../assets/icons/winter_wind.png"),
          sound: require("../assets/sounds/wind/winter.mp3"),
          description: "Winter",
        },
        {
          img: require("../assets/icons/wind_wood.png"),
          sound: require("../assets/sounds/wind/wind_wood.mp3"),
          description: "Wood",
        },
        {
          img: require("../assets/icons/wind_field.png"),
          sound: require("../assets/sounds/wind/wind_grass.mp3"),
          description: "Field",
        },
        {
          img: require("../assets/icons/wind_tree.png"),
          sound: require("../assets/sounds/wind/wind_tree.mp3"),
          description: "tree",
        },
        {
          img: require("../assets/icons/wind_turbine.png"),
          sound: require("../assets/sounds/wind/wind_turbine.mp3"),
          description: "Turbine",
        },
      ],
      isActive: null,

      wind: false,
      fire: false,
      rain: false,
      lighting: false,
      wave: false,
      world: false,
      stopAll: false,

      windVolume: 10,
      fireVolume: 10,
      rainVolume: 10,
      lightingVolume: 10,
      waveVolume: 10,
      worldVolume: 10,

      soundPlay: "",
      firePlay: "",
      rainPlay: "",
      lightingPlay: "",
      wavePlay: "",
      naturePlay: [],
      worldPlay: "",

      allSounds: [],
    };
  },
  methods: {
    getSound(sound, i) {
      if (this.soundPlay != "") {
        this.soundPlay.pause();
      }

      this.soundPlay = new Audio(sound);
      this.soundPlay.dataset.name = this.winds[i].description;
      this.soundPlay.loop = true;

      this.soundPlay.play();

      this.isActive = i;

      this.wind = true;
    },
    stopWind() {
      this.soundPlay.pause();
      this.wind = !this.wind;
    },
    playWind() {
      this.soundPlay.play();
      this.wind = !this.wind;
    },
    stopFire() {
      this.firePlay.pause();
      this.fire = !this.fire;
    },
    playFire() {
      this.firePlay.play();
      this.fire = !this.fire;
    },
    getFire(data) {
      this.firePlay = data;
      this.fire = true;
    },
    stopRain() {
      this.rainPlay.pause();
      this.rain = !this.rain;
    },
    playRain() {
      this.rainPlay.play();
      this.rain = !this.rain;
    },
    getRain(data) {
      this.rainPlay = data;
      this.rain = true;
    },
    stopLighting() {
      this.lightingPlay.pause();
      this.lighting = !this.lighting;
    },
    playLighting() {
      this.lightingPlay.play();
      this.lighting = !this.lighting;
    },
    getLighting(data) {
      this.lightingPlay = data;
      this.lighting = true;
    },
    stopWave() {
      this.wavePlay.pause();
      this.wave = !this.wave;
    },
    playWave() {
      this.wavePlay.play();
      this.wave = !this.wave;
    },
    getWave(data) {
      this.wavePlay = data;
      this.wave = true;
    },
    stopWorld() {
      this.worldPlay.pause();
      this.world = !this.world;
    },
    playWorld() {
      this.worldPlay.play();
      this.world = !this.world;
    },
    getWorld(data) {
      this.worldPlay = data;
      this.world = true;
    },

    getNature(data) {
      this.naturePlay = [...data];
      console.log(this.naturePlay);
    },

    stopAllSounds() {
      this.addToAllSounds();
      this.stopAll = true;

      this.allSounds.forEach((elem) => {
        if (elem) elem.pause();
      });

      this.naturePlay.forEach((elem) => {
        elem.pause();
      });

      this.wind = false;
      this.fire = false;
      this.rain = false;
      this.lighting = false;
      this.wave = false;
      this.world = false;
    },
    playAllSounds() {
      this.stopAll = false;

      this.allSounds.forEach((elem) => {
        if (elem) elem.play();
      });

      this.naturePlay.forEach((elem) => {
        elem.play();
      });

      this.wind = true;
      this.fire = true;
      this.rain = true;
      this.lighting = true;
      this.wave = true;
      this.world = true;
    },
    addToAllSounds() {
      this.allSounds[0] = this.soundPlay;
      this.allSounds[1] = this.firePlay;
      this.allSounds[2] = this.rainPlay;
      this.allSounds[3] = this.lightingPlay;
      this.allSounds[4] = this.wavePlay;
      this.allSounds[5] = this.worldPlay;
    },

    closePanel(){
      document.querySelector('.control_modal').classList.add('hide')
      document.querySelector('.close').style.display = 'none'
      document.querySelector('.show').style.display = 'block'
    },

    showPanel(){
      document.querySelector('.control_modal').classList.remove('hide')
      
      setTimeout(()=>{
        document.querySelector('.close').style.display = 'block'
      }, 500 )
    }
  },

  watch: {
    windVolume() {
      this.soundPlay.volume = this.windVolume / 10;
    },
    fireVolume() {
      this.firePlay.volume = this.fireVolume / 10;
    },
    rainVolume() {
      this.rainPlay.volume = this.rainVolume / 10;
    },
    lightingVolume() {
      this.lightingPlay.volume = this.lightingVolume / 10;
    },
    waveVolume() {
      this.wavePlay.volume = this.waveVolume / 10;
    },
    worldVolume() {
      this.worldPlay.volume = this.worldVolume / 10;
    },
  },
};
</script>



<style>
hr {
  border: 1px solid #70727330;
  width: 80%;
}

main {
  padding-bottom: 100px;
}

h1 {
  font-family: inherit;
  text-transform: uppercase;
}

h3 {
  text-align: left;
  padding: 0 70px;
  color: #435353;
  font-weight: 600;
  font-size: 20px;
}

ul {
  list-style: none;
  padding: 0;
}

.title {
  margin: 0;
  padding: 0;
  font-size: 20px;
  color: #656565;
}

.container {
  width: 100%;
  float: right;
}

/* wind */

.wind,
.fire,
.rain,
.lighting,
.wave,
.nature,
.world {
  width: 10%;
  float: left;
  cursor: pointer;
}

.wind_description,
.fire_description,
.rain_section,
.lighting_section,
.wave_section,
.nature_section,
.world_section {
  font-weight: 700;
  color: #8b8b8b;
}

.active {
  background: aliceblue;
  border-radius: 20px;
}

img {
  width: 45px;
  padding-top: 20px;
}

/* control modal */

.control_modal {
  background: #fff;
  width: 300px;
  min-height: 100px;
  position: fixed;
  right: 70px;
  box-shadow: 1px 3px 5px 0 #4c4c4c69;
  border-radius: 5px;
  transition: .5s linear;
}

.modal_title {
  border-bottom: 1px solid #c7c7c7;
  padding-bottom: 10px;
}

.sound_item {
  display: flex;
  justify-content: space-between;
  padding: 10px 20px;
  align-items: center;
}

.sound_item img {
  padding: 0;
  width: 20px;
  cursor: pointer;
}

.sound_item span {
  font-weight: 700;
  margin-left: 20px;
}

.stop_all {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px;
  background: #c7eced;
  font-weight: 700;
  border-radius: 0 0 5px 5px;
}

.stop_all img {
  width: 28px;
  padding: 0 10px;
  cursor: pointer;
}

.section {
  width: 90%;
  margin: 0 auto;
}

.container.end {
  margin-bottom: 100px;
}

.hide {
  margin-left: -200px;
}


.show {
   position: absolute;
    right: -185%;
    display: none;
}

img.close {
    position: absolute;
    right: -85%;
    width: 25px;
}


/* mobile */

@media (max-width: 400px) {
  .wind,
  .fire,
  .rain,
  .lighting,
  .wave,
  .nature,
  .world {
    width: 30%;
  }

  h3 {
    text-align: center;
  }
  
  h3.control_modal{
    padding: 0;
  }

  .control_modal {
    top: 0;
    left: 0;
    width: 50%;
  }
  .modal_title{
    text-align: center;
  }

  li.sound_item {
    display: contents;
}
}
</style>