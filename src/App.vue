<template>
  <div id="app">
    <p v-if="restrauntNumber==0">近くにお店はありませんでした</p>
    <div v-else v-for="restraunt in restraunts" :key="restraunt.id" class='card'>
      <a :href="restraunt.urls.pc">
          <div class="card-image">
            <img :src="restraunt.logo_image">
          </div>
          <div class="card-title">
            <h3>{{restraunt.name}}</h3>
          </div>
          <div>
            <p>{{restraunt.genre.name}}</p>
          </div>
      </a>
    </div>
    <div>Powered by <a href="http://webservice.recruit.co.jp/">ホットペッパー Webサービス</a></div>
  </div>
</template>

<script>
import jQuery from 'jquery';

export default{
  name:"App",
  data(){
    return{
      restraunts:[],
      isNotFriend:true
    }
  },
  mounted(){
    this.getData();
  },
  methods:{
    getData(){
      var self = this ;//eslint-disable-line
      const success = async function(position){
        const lat = position.coords.latitude;
        const lng = position.coords.longitude;
        const URL ="https://webservice.recruit.co.jp/hotpepper/gourmet/v1/?key=0336bf1d8a990721&lat="+lat+"&lng="+lng+"&range=2&order=4&count=100&count=100&format=jsonp&callback=callback";
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
      navigator.geolocation.getCurrentPosition(success);
    }
  },
  watch:{
    restraunts:function() {
      this.restrauntNumber = this.restraunts.length;
    }
  }
}
</script>

<style>
div{
  margin: 0;
  padding: 0;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #DEDEDE;
  margin: 0;
}
.card{
  margin: 20px;
  padding: 5%;
  max-height: 150px;
  position: relative;
  border-radius: 50px;
  background: #DEDEDE;
  box-shadow:  10px 10px 30px #aeaeae,
              -10px -10px 30px #ffffff;
}
.card:active{

  border-radius: 50px;
  background: linear-gradient(145deg, #cacaca, #f0f0f0);
  box-shadow: 10px 10px 30px #cecece,
              -10px -10px 30px #ffffff;
}
.card-image{
  display: inline-block;
  max-width: 30%;
  vertical-align: middle;
}
image{
  max-width: auto;
  max-height: 100%;
}
.card-title{
  display: inline-block;
  width: 70%;
  vertical-align: middle;
  font-size: 1rem;
}
a{
  text-decoration: none;
  color: #2c3e50;
}
</style>
