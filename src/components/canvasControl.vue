<template>
    <div>
        <canvas id="map"></canvas>
    </div>
</template>

<script>
export default{
  data(){
    return{
      heroid:1,
      hero:{
        id: 1,                  //人物编号
        x: 10,
        y: 10,                 //坐标（x，y）
        width: 32,
        height: 32,            //单个人物的尺寸
        size: 1,              //不同rpg素材图规格不一样。size1:32*32 ,size2:45*60 ,size3:用户自定义
        direction: [ 0, 0],  //第一个参数是方向0-3(size1：下左右上， size2：下左上右)，第二个参数是该方向的动作0-2
      },  
    }
  },
  props: {
    'heroId':{
      type: Number,
      default: 1
    },
  },
  //watch很重要。data（）函数只是在初始化的时候会运行一次。而我们异步过来的数据，需要watch他 才能得到。
  watch:{
    heroId:function(newVal,oldVal){         //不能写成箭头函数，不然监测不到this
      this.hero.id = newVal 
    }
  },
  mounted(){
    var canvas = document.getElementById("map");
    if (canvas.getContext){
       var ctx = canvas.getContext("2d");
       canvas.width = 480;
       canvas.height = 480;

      ctx.clearRect(0,0,480,480)
      var heroImage = new Image()
      heroImage.src = require(`../assets/character/size${this.hero.size}/${this.hero.id}.png`)

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
        if(hero.id < 6){
          hero.size = 1
          hero.width = 32
          hero.height = 32
        }  
        else{
          hero.size = 2
          hero.width = 45
          hero.height = 60
        }  
        heroImage.src = require(`../assets/character/size${hero.size}/${hero.id}.png`) 
        ctx.drawImage(heroImage, hero.width*hero.direction[1], hero.height*hero.direction[0], hero.width, hero.height, hero.x, hero.y, 50, 50)
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
              if(hero.size == 2)  hero.direction[0] = 2
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
              if(hero.size == 2)  hero.direction[0] = 3
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