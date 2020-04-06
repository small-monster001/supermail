<template>
  <div id="home">
    <nav-bar class="nav-home"><div slot="center">购物街</div></nav-bar> 
     <tab-control :title="['流行','新款','精选']"  @itemClick="tabClick" ref="tabcontrol1" class="tabcontrol1" v-show="isShowTabcontrol">
    </tab-control>
   <scroll :probeType="3" ref="scroll" @showbacktop="showbacktop" :pullUpLoad="true" @pullupload="load"> 
      <swiper>
      <swiper-item v-for="(item,index) in banners" :key="index">
        <a :href="item.link"> 
          <img :src="item.image" alt="" @load="swiperLoad">        
        </a>
      </swiper-item>
    </swiper>

    <recommend-view :recommends="recommends">
    </recommend-view>

    <feature-view>
    </feature-view>

    <tab-control :title="['流行','新款','精选']"  @itemClick="tabClick" ref="tabcontrol">
    </tab-control>
    
    <goods-list :goodsdata="goods[typedata].list">

    </goods-list>
   </scroll>
   <back-top @click.native="backClick" v-show="isShow">

   </back-top>
    <div class="zhan"></div> 
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar"
import {Swiper,SwiperItem} from "components/common/swiper/index"
import RecommendView from "./homeChildren/Recommend"
import FeatureView from "./homeChildren/Feature"
import TabControl from "components/contents/tabcontrol/TabControl.vue"
import GoodsList from "components/contents/goods/GoodsList.vue"
import Scroll from "components/common/scroll/Scroll.vue"
import BackTop from "components/contents/backtop/BackTop.vue" 


import {getHomeMultidata,getHomeData} from "@/network/home.js"
export default{
 name:'home',
 components:{
   NavBar,
   Swiper,
   SwiperItem,
   RecommendView,
   FeatureView,
   TabControl,
   GoodsList,
   Scroll,
   BackTop
 },
 data(){
  return{
    banners:[],
    recommends:[],
    goods:{
      'pop':{page:0,list:[]},
      'new':{page:0,list:[]},
      'sell':{page:0,list:[]}
    },
    typedata:"pop",
    isShow:false,
    isSwiperLoad:false,
    isShowTabcontrol:false
  } 
 },
 created(){
  this.getHomeMultidata(),
  this.getHomeData("pop"),
  this.getHomeData("new"),
  this.getHomeData("sell")
 },
 methods:{
  //子组件相关
  tabClick(index){
    switch(index){
      case 0 : this.typedata="pop"
       break
      case 1 : this.typedata="new"
       break
      case 2 : this.typedata="sell"
    }
    this.$refs.tabcontrol1.currentIndex=index;
    this.$refs.tabcontrol.currentIndex=index;
  },
  backClick(){
    this.$refs.scroll.backtop();  
  
  }, 
  showbacktop(position){
     this.isShow=(-position.y)>600;
     if(this.isSwiperLoad){
      //  console.log(this.$refs.tabcontrol.$el.offsetTop);
       this.isShowTabcontrol=-position.y>(this.$refs.tabcontrol.$el.offsetTop+44)
     }
  },
  load(){
    this.getHomeData(this.typedata);
    console.log("下拉加载更多")
    this.$refs.scroll.finishPullUp()
  },
  swiperLoad(){
    this.isSwiperLoad=true;
  },
  // 网络请求相关
   getHomeMultidata(){
      getHomeMultidata().then(res=>{
      // console.log(res.data);
      // console.log(res.data.banner);
      // console.log(res.data.recommend)
      this.banners=res.data.banner.list;
      this.recommends=res.data.recommend.list;
     })
   },
   getHomeData(type){
     const page=this.goods[type].page+1;
     getHomeData(type,page).then(res=>{
      //  console.log(res.data)
       this.goods[type].list.push(...res.data.list);
       this.goods[type].page++;
     })  
   }
 },
 mounted(){
   
   this.$bus.$on("imageLoad",()=>{
     console.log('图片加载完成');
     this.$refs.scroll.refresh();
   })
 }
//  computed:{
//    isShow(){
//      return (-this.$refs.scroll.scroll.position.y)>500 
//    }s
//  }
}
</script>


<style scoped>
.nav-home{
  background-color:var(--color-tint);
  color:var(--color-background);
/* 
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 2; */
}
#home{
  position: relative;
  /* height: 100vh; */
}
.tabcontrol1{
  position: relative;
  z-index: 3;
}

.zhan{
  padding-bottom: 1000px;
}
</style>