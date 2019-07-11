<template>
  <div id="app">
    <SoundSketch msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import SoundSketch from './components/SoundSketch.vue'

export default {
  name: 'app',
  components: {
    SoundSketch
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
  }
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /*margin-top: 60px;*/
  display: flex;
  width: 100%;
  height: 100vh;
}
</style>
