<template>
  <div id="home">
    <!--    顶部navbar-->
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>

  <!--    轮播图-->
    <home-swiper :banners="banners"></home-swiper>

    <recommend-view :recommends="recommends"></recommend-view>

    <feature-view></feature-view>

    <teb-control :titles="['流行','新款','精选']"></teb-control>


    <ul>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
      <li>1</li>
    </ul>

  </div>
</template>

<script>
import NavBar from "../../components/common/navbar/NavBar";
import HomeSwiper from "./childComps/HomeSwiper";
import RecommendView from "./childComps/RecommendView";
import FeatureView from "./childComps/FeatureView";

import {getHomeMultidata} from "../../network/home";
import TebControl from "../../components/content/tabControl/TebControl";


export default {
  name: "Home",
  components:{
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TebControl
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
      this.recommends=res.data.recommend.list;
      })
  }

}
</script>

<style scoped>
#home {
  padding-top: 44px;
  height: 100vh;
  position: relative;
}
.home-nav{
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  z-index: 9;
  background-color: var(--color-tint);
  color: #ffffff;
}
</style>
