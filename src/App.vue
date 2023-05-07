<template>
  <h1>Dark & Darker pick locking training</h1>
  <p>On the first time you click Start it might show error. Just close it and then you can play.</p>
  <p>Instruction: Click Start Opening button</p>
  <p> Wait while Picking Lock bar is filling and press SPACE in right moment</p>
  <p>   Judge for yourself whether you clicked at the right moment and Click Try Again</p>
 <p> Repeat </p>
<!-- <ChestOpening/> -->
  <HelloWorld/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
// import ChestOpening from './components/ChestOpening.vue'


export default {
  name: 'App',
  components: {
    HelloWorld,
    // ChestOpening
  }
}
</script>

<style>
body, html {
  height: 100%;
  background-image: url("./assets/bcg.PNG");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #d5d100;
}
</style>
