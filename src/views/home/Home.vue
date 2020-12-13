<template>
  <div id="home">
    <!--    顶部navbar-->
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>

    <scroll class="content" ref="scroll" :probe-type="3"
            @scroll="contentScroll"
            :pull-up-load="true"
            @pullingUp="loadMore">
      <!--    轮播图-->
      <home-swiper :banners="banners"></home-swiper>

      <recommend-view :recommends="recommends"></recommend-view>

      <feature-view></feature-view>

      <teb-control :titles="['流行','新款','精选']"
                   class="tab-control"
                   @tabClick="tabClick">
      </teb-control>

      <goods-list :goods="showGoods"></goods-list>


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
    </scroll>
    <back-top @click.native="backClick" v-show="isShowBackTop"></back-top>
  </div>
</template>

<script>
import NavBar from "../../components/common/navbar/NavBar";
import HomeSwiper from "./childComps/HomeSwiper";
import RecommendView from "./childComps/RecommendView";
import FeatureView from "./childComps/FeatureView";

import {getHomeMultidata} from "../../network/home";
import {getHomeGoods} from "../../network/home";
import TebControl from "../../components/content/tabControl/TebControl";
import GoodsList from "../../components/content/goods/GoodsList";

import Scroll from "../../components/common/scroll/Scroll";
import BackTop from "../../components/content/backTop/BackTop";

export default {
  name: "Home",
  components:{
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TebControl,
    GoodsList,
    Scroll,
    BackTop
  },
  data(){
    return{
      banners:[],
      recommends:[],
      //下面商品的数据结构
      goods:{
        'pop':{page:0,list:[]},
        'new':{page:0,list:[]},
        'sell':{page:0,list:[]},
      },
      currentType:'pop',
      isShowBackTop:false
    }
  },
  computed:{
    showGoods(){
      return this.goods[this.currentType].list
    }
  },
  created() {
  //1.请求多个数据
    this.getHomeMultidata()
    //请求下面流行,新款,精选的商品数据
    this.getHomeGoods('pop')
    this.getHomeGoods('sell')
    this.getHomeGoods('new')

    //监听item图片加载完成(goodsslistitem组件中发射出的事件总线)
    this.$bus.$on('itemImageLoad',()=>{
          this.$refs.scroll.scroll.refresh()
    })
  },
  methods:{
    //事件监听相关方法
    tabClick(index){
      //console.log(index);
      switch(index){
        case 0:
          this.currentType='pop'
          break
        case 1:
          this.currentType='new'
          break
        case 2:
          this.currentType='sell'
          break
      }
    },

    //点击图标回到顶部
    backClick(){
      this.$refs.scroll.scrollTo(0,0,300)
    },

    contentScroll(position){
     // console.log(position)
     //  this.isShowBackTop = (-position.y) > 1000

      this.isShowBackTop = (-position.y) > 1000
    },

    //上拉加载更多
    loadMore(){
      console.log(223);
      this.getHomeGoods(this.currentType)
      this.$refs.scroll.scroll.refresh()
    },

    //网络请求相关方法
    getHomeMultidata(){
    getHomeMultidata().then(res=>{
      console.log(res.data);
      this.banners=res.data.banner.list;
      this.recommends=res.data.recommend.list;
    })
    },

    getHomeGoods(type){
      const page=this.goods[type].page+1
      getHomeGoods(type,page).then(res=>{
        console.log(res);

        this.goods[type].list.push(...res.data.list)
        this.goods[type].page+1

      })
    }

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
.tab-control {
  position: sticky;
  top: 44px;
}
/*.content{*/
/*  height: calc(100% - 93px);*/
/*  overflow: hidden;*/
/*  !*margin-top: 50px;*!*/
/*}*/

.content {
  overflow: hidden;

  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
}
</style>
