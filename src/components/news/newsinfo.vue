<template>
  <div id="newsinfo" v-show="showflag">
    <div class="tmzhead">
      <div class="tmzheadtitle">
        <p>{{news.title}}</p>
        <!--<p>福建省大放送大佛的事</p>-->
      </div>
    </div>


    <div class="tmzbody1">
      <iframe id="tbf" :src="news.url" scrolling="auto"></iframe>
    </div>
    <div class="back" @click="back">
      <img src="../../assets/back.png">
    </div>
    <!--<div>-->
    <!--<back></back>-->
    <!--</div>-->
  </div>
</template>

<script>
  import {Indicator1} from 'mint-ui'

  export default {
    data () {
      return {
        showflag: false
      }
    },
    props: {
      news: {
        type: Object
      }
    },
    mounted: function () {
      document.getElementById('tbf').style.height = window.innerHeight - 37 + 'px';
      document.getElementById('tbf').style.width = window.innerWidth - 0 + 'px';
//            document.getElementById("tbf").src = "http://mini.eastday.com/mobile/170726155824378.html";
    },
    methods: {
      show(){
        this.showflag = true;
      },
      back(){
        this.showflag = false;
      }
    },
    components: {
//            back
    }
  }
</script>

<style>
  #newsinfo {
    position: absolute;
    top: 0px;
    left: 0px;
    z-index: 50;
    width: 100%;
    background-color: white;
    /*border: solid 1px black;*/
  }

  #newsinfo {
    animation: myfirst 0.3s linear 0s infinite alternate;
    animation-iteration-count: 1;
  }

  @keyframes myfirst {
    0% {
      background: red;
      left: 100%;
      top: 0px;
    }
    100% {
      background: blue;
      left: 0px;
      top: 0px;
    }
  }

  /*.tmzheadtitle{*/
  /*font-size: 20px;*/
  /*text-align: center;*/
  /*}*/

  .tmzbody1 {
    position: absolute;
    top: 36px;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
    background-color: white;
    display: block;
    /*border: solid 1px white;*/
  }

  #tbf {
    /*margin-top: 2px;*/
    display: block;
    background: white;
  }

  .back {
    position: fixed;
    /*margin-left: -200px;*/
    /*margin-top: 50%;*/
    left: 10px;
    top: 50%;
    display: inline-block;
    background: rgba(0, 0, 0, 0.5);
    border-radius: 50%;
    text-align: center;
    /*z-index: 90;*/
    width: 50px;
    height: 50px;
  }

  .back img {
    margin-right: 10px;
    margin-top: 10px;
    width: 30px;
    height: 30px;
  }
</style>
