<template>
 <div class="recommend">
   <div v-for="item in recommends" v-bind:key="item.sort" class="recommend-item">
     <a :href="item.link">
       <img :src="item.image" alt="">
       <div>{{item.title}}</div>
     </a>
   </div>
 </div>
</template>

<script>
export default {
name: "RecommendView",
  props:{
  recommends:{
  type:Array,
    default(){
    return []
    }
  }
  }
}
</script>

<style scoped>
.recommend{
  display: flex;
  text-align: center;
  margin-bottom: 10px;
  font-size: 12px;
  padding: 10px 0 15px;
  border-bottom: 8px solid #EEEEEE;

}
.recommend-item{
  flex: 1;
}
.recommend-item img{
  width: 70px;
  height: 70px;
}


</style>
