<template>
  <div id="app">
    <Clicker msg="Welcome to Reservix-Clicker 0.1.2"/>
  </div>
</template>

<script>
import Clicker from './components/Clicker.vue'

export default {
  name: 'app',
  components: {
    Clicker
  }
}
</script>

<style lang="scss">
#app {
  font-family: sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
