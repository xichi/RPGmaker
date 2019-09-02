<template>
  <div id="app">
    <canvasControl/>
  </div>
</template>

<script>
import canvasControl from './components/canvasControl.vue'
export default {
  name: 'app',
  components: {
    canvasControl
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
