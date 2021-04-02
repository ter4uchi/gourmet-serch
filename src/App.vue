<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png">
    <a href="http://webservice.recruit.co.jp/"><img src="http://webservice.recruit.co.jp/banner/hotpepper-s.gif" alt="ホットペッパー Webサービス" width="135" height="17" border="0" title="ホットペッパー Webサービス"></a>
  </div>
</template>

<script>
//import { Options } from '../node_modules/vue-class-component/dist/vue-class-component';
export default{
  name:"App",
  data(){
    return{

    }
  },
  created(){
    console.log("location");
      const success = function(position){
        console.log(position)
        console.log(position.coords.latitude);
        console.log(position.coords.longitude);
      }
    navigator.geolocation.getCurrentPosition(success)
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
