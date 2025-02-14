<template>
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
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
  margin-top: 60px;
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

body {
  background-image: linear-gradient(to bottom right, #ffb6c1, #C177B2);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
