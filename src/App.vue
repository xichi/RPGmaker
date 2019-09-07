<template>
  <div id="app">
    <canvasControl :heroId="heroId"/>
    <button @click="charC">改变人物</button>
  </div>
</template>

<script>
import canvasControl from './components/canvasControl.vue'
export default {
  name: 'app',
  data(){
    return{
      heroId: 1
    }
  },
  components: {
    canvasControl
  },
  methods:{
    charC(){
       this.heroId = ( this.heroId + 1 )%10
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
