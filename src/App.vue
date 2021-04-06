<template>
  <div>
    <div v-for="restraunt in restraunts" :key="restraunt.id" class='card'>
      <a :href="restraunt.urls.pc">{{restraunt.name}}
        {{restraunt.genre.name}}
        <img :src="restraunt.logo_image">
      </a>
    </div>
    Powered by <a href="http://webservice.recruit.co.jp/">ホットペッパー Webサービス</a>
  </div>
</template>

<script>
import jQuery from 'jquery';

export default{
  name:"App",
  data(){
    return{
      restraunts:null,

    }
  },
  mounted(){
    this.getData();
  },
  methods:{
    getData(){
      var self = this ;//eslint-disable-line
      const success = function(position){
      const lat = position.coords.latitude;
      const lng = position.coords.longitude;
      const URL ="https://webservice.recruit.co.jp/hotpepper/gourmet/v1/?key=0336bf1d8a990721&lat="+lat+"&lng="+lng+"&range=2&order=4&format=jsonp&callback=callback";
      jQuery.ajax({
        type: 'GET',
        url: URL,
        dataType: 'jsonp',
        jsonpCallback:'callback',
        success: out => {
          self.restraunts = out.results.shop;
        }
      });
      }
      navigator.geolocation.getCurrentPosition(success)
    }
  },
  watch:{
    restraunts:function() {
      console.log(this.restraunts);
    }
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
  display: flex;            /* Flexboxを指定 */
  justify-content: center;  /* 水平方向の中央寄せ */
}
.card{
  margin: 4%;
  height: 150px;
  border-radius: 50px;
  background: #e0e0e0;
  box-shadow:  10px 10px 30px #bebebe,
              -10px -10px 30px #ffffff;
}
.card:active{
  margin: 2%;
  border-radius: 50px;
  background: linear-gradient(145deg, #cacaca, #f0f0f0);
  box-shadow:  10px 10px 30px #bebebe,
              -10px -10px 30px #ffffff;
}
a{
  display: block;
  text-decoration: none;
  color: #2c3e50;
}
</style>
