<template>
  <div id="app">
    <logo></logo>
    <tmzmenu></tmzmenu>
  </div>
</template>

<script>
  import menu from './components/menu/menu.vue'
  import logo from './components/menu/logo.vue'

  export default {
    name: 'app',
    data () {
      return {

      }
    },
    methods: {

    },
    components: {
      'tmzmenu':menu,
      logo
    }
  }
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    backgroud: blue;
    color: white;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 120px;
  }

  .tmzhead{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 36px;
    background-color: #7e57c2;
    text-align: left;
    z-index: 20;
  }
  .logo{
    flex: 0 0 76px;
  }
  .blank{
    flex: 0 0 50px;
    width: 50px;
  }
  .tmzheadtitle{
    flex: 1;
    width: auto;
    font-size: 24px;
    margin-top: 4px;
    margin-right: 30px;
    margin-left: 50px;
    height: 30px;
    overflow: auto;
    /*float: left;*/
    text-align: center;
  }
  .tmzbody{
    position: absolute;
    top: 36px;
    left: 0;
    bottom: 56px;
    width: 100%;
    /*margin-bottom: 80px;*/
    z-index: 10;
    /*border: solid 3px black;*/
    overflow-y: scroll;
    padding:0 8px;
  }
</style>
