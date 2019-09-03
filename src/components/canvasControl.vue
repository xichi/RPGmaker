<template>
    <div>
        <canvas id="map"></canvas>
    </div>
</template>

<script>
export default{
  data(){
    return{
      hero:{
        id: 1,
        x: 10,
        y: 10,
        width: 32,
        direction: [ 0, 0],  //第一个参数是方向0-3(上下左右)，第二个参数是该方向的动作0-2
      },  
    }
  },
  props:{
     
  },
  mounted(){
    var canvas = document.getElementById("map");
    if (canvas.getContext){
       var ctx = canvas.getContext("2d");
       canvas.width = 480;
       canvas.height = 480;

      ctx.clearRect(0,0,480,480)
      var heroImage = new Image()
      heroImage.src = require(`../assets/character/${this.hero.id}.png`)

      keyboard(ctx,this.hero)
      setInterval(()=>{
         update(ctx,this.hero,heroImage)
       },100);   
      setInterval(()=>{
         move(this.hero)
      },500)
      
    }
    //渲染到画布上
   /*  function render(ctx,hero){
        ctx.clearRect(0,0,480,480)
        var heroImage = new Image(1,1)
        heroImage.onload = function (){
          ctx.drawImage(heroImage, hero.x, hero.y)
        }
        heroImage.src = require('../assets/hero.png')
     }
 */
    //更新渲染
    function update(ctx,hero,heroImage){
        ctx.clearRect(0,0,480,480)
        ctx.drawImage(heroImage, hero.width*hero.direction[1], hero.width*hero.direction[0], hero.width, hero.width, hero.x, hero.y, 50, 50)
    }
    function move(hero){   //人物行走
        hero.direction[1] =  ( hero.direction[1] + 1 ) % 3
    }

    //键盘控制
    function keyboard(ctx,hero){
        addEventListener("keydown",function(e){
          switch(e.keyCode){
            case 38:
              hero.y -= 5
              hero.direction[0] = 3
               break
            case 40:
              hero.y += 5
              hero.direction[0] = 0
              break
            case 37:
              hero.x -= 5
              hero.direction[0] = 1
              break
            case 39:
              hero.x += 5
              hero.direction[0] = 2
              break
          }
        })
      }
    
    }


 }

</script>

<style lang="stylus" scoped>
  #map
   margin:0 auto 
   border:1px solid #000
</style>