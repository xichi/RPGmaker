<template>
    <div>
        <canvas id="map"></canvas>
    </div>
</template>

<script>
export default{
  mounted(){
    var canvas = document.getElementById("map");
    var ctx = canvas.getContext("2d");
    canvas.width = 480;
    canvas.height = 480;
 }
}
</script>

<style lang="stylus" scoped>
  #map
   margin:0 auto 
   background-color:pink
</style>