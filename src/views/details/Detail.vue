<template>
  <div id="detail">
    <nav-bar>
      <div slot="left" class="navbar-left" @click="backClick">
        <img src="~assets/img/common/back.svg" alt="">
      </div>
      <div slot="center" class="detail-navbar">
          <div 
          v-for="(item,index) in navbarData" 
          :key="index" 
          class="navbar-center" 
          :class="{'navbar-active':currentIndex==index}"
          @click="itemClick(index)"
        >{{item}}</div> 
      </div>
    </nav-bar>

    <swiper class="detail-swiper">
      <swiper-item v-for="(item) in imgTop" :key="item.id">         
          <img :src="item" alt="">
      </swiper-item>
    </swiper>
    <Middle :goods="goods" :goodsparam="goodsparam" :shop="shop">

    </Middle>
    <h2>sad {{this.$route.query}}</h2>
  </div>
</template>

<script>
// import axios from "network/axios.js"
import NavBar from "components/common/navbar/NavBar.vue"
import {Swiper,SwiperItem} from "components/common/swiper/index.js"
import Middle from "./detailChildren/Middle.vue"

import {getDetail,getRecommend,Goods,GoodsParam,Shop} from "network/detail.js"
export default{
  name:'Detail',
  data(){
    return{
      iid:null,
      data:{},
      navbarData:["商品","参数","评论","推荐"],
      currentIndex:0,
      imgTop:[],
      goods:{},
      goodsparam:{},
      shop:{}
    }
  },
  components:{
    NavBar,
    Swiper,
    SwiperItem,
    Middle
  },
  created(){
    // this.iid=this.$route.query.iid
    
    // axios({
    //   url:'/detail',
    //   params:{
    //     iid:this.$route.query.iid
    //   }
    // }).then(res=>{
    //   console.log(res)   
    // })
    getDetail(this.$route.query.iid).then(res=>{
      console.log(res);
      this.data=res.result;
      this.goods=new Goods(this.data.itemInfo,this.data.columns,this.data.shopInfo.services); 
      this.goodsparam=new GoodsParam(this.data.itemParams.info,this.data.itemParams.rule);
      this.shop=new Shop(this.data.shopInfo)
      this.imgTop=res.result.itemInfo.topImages
    })
   
  },
  mounted(){  
    
  },
  methods:{
    itemClick(index){
      this.currentIndex=index;
    },
    backClick(){
      this.$router.go(-1);
    }
  }
  
}
</script>

<style scoped>
.detail-navbar{
  display: flex;
}
.navbar-center{
  flex:1;
}
.navbar-active{
  color: red;
}
.navbar-left{
  margin-top: 5px;
}
.detail-swiper{
  height: 300px;
}
</style>