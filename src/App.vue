<template>
  <div id="app">
    <canvasControl :hero="hero"/>
    <button @click="charC">改变人物</button>
  </div>
</template>

<script>
import canvasControl from './components/canvasControl.vue'
export default {
  name: 'app',
  data(){
    return{
       hero: {
          id: 2
       },
    }
  },
  components: {
    canvasControl
  },
  methods:{
    charC(){
       
    }
  }
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
