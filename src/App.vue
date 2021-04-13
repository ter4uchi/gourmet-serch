<template>
  <div>
    <loading-overlay class="over"/>
    <p v-if="restrauntNumber==0">近くにお店はありませんでした</p>
    <div v-if="isNotFriend==true">
    <div v-for="restraunt in restraunts" :key="restraunt.id" class='card'>
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
    </div>
    Powered by <a href="http://webservice.recruit.co.jp/">ホットペッパー Webサービス</a>
  </div>
</template>

<script>
import jQuery from 'jquery';
import LoadingOverlay from './components/LoadingOverlay'
//import Card from '../../smartTemplate/src/components/Card.vue';

export default{
  name:"App",
  components:{
    LoadingOverlay
  },
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
        const URL ="https://webservice.recruit.co.jp/hotpepper/gourmet/v1/?key=0336bf1d8a990721&lat="+lat+"&lng="+lng+"&range=2&order=4&count=100&format=jsonp&callback=callback";
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
      console.log(this.restraunts);
      this.restrauntNumber = this.restraunts.length;
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
  background: #DEDEDE;
  /*
  display: flex;            /* Flexboxを指定 
  justify-content: center;  /* 水平方向の中央寄せ */
}
.card{
  margin: 5%;
  padding: 5%;
  max-height: 150px;
  position: relative;
  border-radius: 50px;
  background: #DEDEDE;
  box-shadow:  10px 10px 30px #aeaeae,
              -10px -10px 30px #ffffff;
}
.card:active{
  margin: 5%;
  padding: 5%;
  height: auto;
  border-radius: 50px;
  background: linear-gradient(145deg, #cacaca, #f0f0f0);
  box-shadow: 10px 10px 30px #cecece,
              -10px -10px 30px #ffffff;
}
.card-image{
  display: inline-block;
  max-width: 30%;
}
image{
  max-width: auto;
  max-height: 100%;
}
.card-title{
  display: inline-block;
  width: 70%;
}
a{
  text-decoration: none;
  color: #2c3e50;
}
</style>
