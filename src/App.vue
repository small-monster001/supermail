<template>
  <div id="app">
  <tabBar>
    <tabBarItem path="/home" abc="red">  
        <img slot="item-icon" src="~assets/img/tabbar/home.svg" alt="">
        <img slot="item-icon-active" src="~assets/img/tabbar/home_active.svg" alt="">
        <div slot="item-text">首页</div>      
    </tabBarItem>
    <tabBarItem path="/category" abc="red">    
        <img slot="item-icon" src="~assets/img/tabbar/category.svg" alt="">
        <img slot="item-icon-active" src="~assets/img/tabbar/category_active.svg" alt="">
        <div slot="item-text">分类</div> 
    </tabBarItem>
    <tabBarItem path="/shopcart" abc="red">    
        <img slot="item-icon" src="~assets/img/tabbar/shopcart.svg" alt="">
        <img slot="item-icon-active" src="~assets/img/tabbar/shopcart_active.svg" alt="">
        <div slot="item-text">购物车</div>
    </tabBarItem>
    <tabBarItem path="/profile" abc="red">     
        <img slot="item-icon" src="~assets/img/tabbar/profile.svg" alt=""> 
        <img slot="item-icon-active" src="~assets/img/tabbar/profile_active.svg" alt="">
        <div slot="item-text">我的</div>    
    </tabBarItem>   
  </tabBar>
  <keep-alive>
     <router-view></router-view>
  </keep-alive>
 
  </div>
</template>

<script>
import TabBarItem from "@/components/common/tabBar/TabBarItem.vue"
import TabBar from "@/components/common/tabBar/TabBar.vue"
export default {
  name: 'App',
  components: {
  TabBar,
  TabBarItem
  }
}
</script>

<style>

@import "assets/css/base.css";
</style>
