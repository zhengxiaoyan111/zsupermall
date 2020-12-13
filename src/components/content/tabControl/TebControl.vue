<template>
 <div class="tab-control">
   <div v-for="(item,index) in titles"
        v-bind:key="item"
        class="teb-control-item"
        :class="{active:index===currentIndex}"
        @click="itemClick(index)">
     <span>{{item}}</span>
   </div>
 </div>
</template>

<script>
export default {
  name: "TebControl",
  data(){
   return{
     //记录当前选中的下标值
     currentIndex:0
   }
  },
  props:{
  titles:{
    default(){
      return []
    }
  }
  },
  methods:{
    itemClick(index){
     // console.log(index);
      this.currentIndex=index
      this.$emit('tabClick',index)
    }
  }
}
</script>

<style scoped>
.tab-control{
  display: flex;
  text-align: center;
  font-size: 15px;
  background-color: #fff;
}
.teb-control-item{
  flex: 1;
  height: 40px;
  line-height: 40px;
}
.active{
  color: var(--color-high-text);

}
.active span {
  border-bottom: 3px solid var(--color-high-text);
  padding: 5px 10px;
}
</style>
