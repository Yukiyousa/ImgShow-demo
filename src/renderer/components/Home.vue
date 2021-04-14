<template>
  <div id="wrapper">
    <div>
    <div v-show="isTap">
    <transition-group name="list" tag="ul" mode="out-in">
      <li v-for="(item,index) in piclist" :key="item.url" :style="config[index]" >
        <img :src="item.url" id="img" >
      </li>
    </transition-group>
    </div>
    <div v-show="!isTap">
      <div align="center" class="show">
        <img :src="piclist[currentIndex].url" id="showimg" class="show_img">
      </div>
    </div>
    </div>
  </div>
</template>
<script>

export default {
  data() {
    return {
      piclist: [
        { url: "../../dist/electron/static/image/1.jpg",id:0},
        { url: "../../dist/electron/static/image/2.jpg",id:1},
        { url: "../../dist/electron/static/image/3.jpg",id:2},
        { url: "../../dist/electron/static/image/4.jpg",id:3},
        { url: "../../dist/electron/static/image/5.jpg",id:4},
      ],
      //文件图片配置
config: [
        {
          position: "absolute",
          top: "10vh",
          left: "18vw",
          opacity: 0.4,
          zIndex: 2,
          transition: "all 1s",
          // display:"flex"
        },
        {
          position: "absolute",
          top: "25vh",
          left: "10vw",
          opacity: 0.8,
          zIndex: 3,
          transition: "all 1s",
        },
        {
          position: "absolute",
          top: "40vh",
          left: "35vw",
          opacity: 1,
          zIndex: 4,
          transition: "all 1s",
        },
        {
          position: "absolute",
          top: "25vh",
          left: "60vw",
          opacity: 0.8,
          zIndex: 3,
          transition: "all 1s",
        },
        {
          position: "absolute",
          top: "10vh",
          left: "52vw",
          opacity: 0.4,
          zIndex: 2,
          transition: "all 1s",
        }
        
      ],
      previous: 0,
      gesture:'',
      isTap:true,
      currentIndex:2
    };
  },
  mounted(){
    var ws = new WebSocket("ws://127.0.0.1:5678/");
    var that = this
    ws.onmessage = function(e){
      that.$data.gesture = e.data;
      console.log(that.gesture)
      that.turnright()
      that.maxFun()
      that.minFun()
      that.imgRotate()
      that.showImg()
    }
  },
  methods: {
    turnright: function() {
      if(this.gesture === 'mov'){
        this.config.unshift(this.config.pop());
        if(this.currentIndex < 4){
          this.currentIndex = this.currentIndex + 1
        }else{
          this.currentIndex = 0
        }
        console.log(this.currentIndex)
      }
    },
    maxFun(){
      if(this.gesture === 'grab'){
        var width = document.getElementById('showimg').width
        var height = document.getElementById('showimg').height
        document.getElementById('showimg').style.width = width * 1.25 + 'px'
        document.getElementById('showimg').style.height = height * 1.25 + 'px'
      }
    },
    minFun(){
      if(this.gesture === 'zoom'){
        var width = document.getElementById('showimg').width
        var height = document.getElementById('showimg').height
        document.getElementById('showimg').style.width = width * 0.8 + 'px'
        document.getElementById('showimg').style.height = height * 0.8 + 'px'
      }
    },
    imgRotate(){
      if(this.gesture === 'turn'){
        var n=0
        var i=1
        var time = setInterval(function(){
        n = n + 5
        if(n==360*i){
          i++
          clearInterval(time)
        }
        document.getElementById('showimg').style.transform= "rotate("+n+"deg)"
        },10)
      }
    },
    showImg(){
      if(this.gesture === 'tap'){
        this.isTap = false
      }
    }
  },
};
</script>
<style scoped>

* {
  margin: 0;
  padding: 0;
}
#wrapper {
  margin: auto;
  height: 500px;
  position: relative;
  margin-left: auto;
  margin-right: auto;
}
ul {
  list-style: none;
}
li {
  background-repeat: no-repeat;
}
li img {
  height: 16.6vw;
  width: 30vw;
  border-radius: 10px;
}
.right{
  position:absolute;
  top:50%;
  width:50px;
  height:50px;
  background-color:rgba(0,0,0,.3);
  border-radius:50%;
  cursor:pointer;
  overflow: hidden;
  text-decoration: none;
  z-index: 5;
  opacity: 1;
}
.right{
  right:3%;
  padding-right:12px;
  padding-top:10px;
}
.show_img{
  margin: auto;
  border-radius: 10px;
}
.show{
    padding-top: 20vh;
}

</style>

