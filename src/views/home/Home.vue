<template>
  <div id="home">
    <nav-bar class="nav-home"><div slot="center">购物街</div></nav-bar> 

    <swiper>
      <swiper-item v-for="(item,index) in banners" :key="index">
        <a :href="item.link">
          <img :src="item.image" alt="">        
        </a>
      </swiper-item>
    </swiper>

    <recommend-view :recommends="recommends">

    </recommend-view>
    <feature-view>

    </feature-view>
  </div>
</template>

<script>
import NavBar from "@/components/common/navbar/NavBar"
import {Swiper,SwiperItem} from "@/components/common/swiper/index"
import RecommendView from "./homeChildren/Recommend"
import FeatureView from "./homeChildren/Feature"

import {getHomeMultidata} from "@/network/home.js"
export default{
 name:'home',
 components:{
   NavBar,
   Swiper,
   SwiperItem,
   RecommendView,
   FeatureView
 },
 data(){
  return{
    banners:[],
    recommends:[]
  } 
 },
 created(){
   getHomeMultidata().then(
     res=>{
      // console.log(res.data);
      // console.log(res.data.banner);
      console.log(res.data.recommend)
      this.banners=res.data.banner.list;
      this.recommends=res.data.recommend.list;
     }
   )
 }
}
</script>


<style scoped>
.nav-home{
  background-color:var(--color-tint);
  color:var(--color-background);

  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 2;
}
</style>