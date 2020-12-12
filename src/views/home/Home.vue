<template>
  <div id="home">
    <!--    顶部navbar-->
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>

  <!--    轮播图-->
    <home-swiper :banners="banners"></home-swiper>

  </div>
</template>

<script>
import NavBar from "../../components/common/navbar/NavBar";
import HomeSwiper from "./childComps/HomeSwiper";

import {getHomeMultidata} from "../../network/home";



export default {
  name: "Home",
  components:{
    NavBar,
    HomeSwiper
  },
  data(){
    return{
      banners:[],
      recommends:[]
    }
  },
  created() {
  //1.请求多个数据
    getHomeMultidata().then(res=>{
      console.log(res.data);
      this.banners=res.data.banner.list;
      this.recommends=res.data.recommend;
      })
  }

}
</script>

<style scoped>
#home {
  /*padding-top: 44px;*/
  height: 100vh;
  position: relative;
}
.home-nav{
  background-color: var(--color-tint);
  color: #ffffff;
}
</style>
