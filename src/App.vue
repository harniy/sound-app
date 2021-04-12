<template>
  <div id="app">

    <Sound />

  </div>
</template>

<script>
import Sound from './components/sound'

export default {
  name: 'App',
  components: {
    Sound
  },
  data(){
    return{
     
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body{
  background: #ffeb3bc4;
}

</style>
