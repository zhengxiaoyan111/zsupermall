<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
export default {
  name: "Scroll",
  props:{
    probeType: {
      type:Number,
      default:0
    }
  },
  data(){
    return{
      scroll:null,
      message:'哈哈哈'
    }
  },
  mounted() {
    //创建BScroll对象
    this.scroll=new BScroll(this.$refs.wrapper,{
        click:true,
      probeType:3
    })
    //监听滚动的位置
    this.scroll.on('scroll',(position)=>{
      // console.log(position);
      this.$emit('scrol',position)
    })

  },
  methods:{
    scrollTo(x,y,time){
      this.scroll.scrollTo(x,y,time)
    }
  }
}
</script>

<style scoped>

</style>
