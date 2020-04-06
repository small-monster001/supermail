<template>
  <div ref="wrapper" class="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll"
export default{
  name:"Scroll",
  data(){
    return{
      scroll:null   
    }
  },
  props:{
    probeType:{
        type:Number,
        default:0
    },
    pullUpLoad:{
      type:Boolean,
      default:true
    }
  },
  mounted(){
    this.scroll=new BScroll(this.$refs.wrapper,{
      probeType:this.probeType,
      click:true,
      pullUpLoad:this.pullUpLoad
    })
    this.scroll.on("scroll",position=>{
      // console.log(position);
      // 要监听了才能得到位置数据
      this.$emit("showbacktop",position)  
    })
    this.scroll.on("pullingUp",()=>{
      this.$emit("pullupload"); 
    })
  },
  methods:{
    backtop(){
      this.scroll&&this.scroll.scrollTo(0,0)
    },
    finishPullUp(){
      this.scroll&&this.scroll.finishPullUp();
    },
    refresh(){
      this.scroll&&this.scroll.refresh();
    }
  }
 
}
</script>

<style scoped>
.wrapper{
  position:absolute;
  top: 44px;
  left: 0;
  right: 0;
  bottom: 49px;
  overflow: hidden; 
}
/* .wrapper{
  height: calc(100vh - 93px);
  overflow: hidden;
  margin-top: 44px;
  margin-bottom: 49px;
} */
</style>