<template>
 <div id="recommendView">
   <div class="recommend-item" v-for="(item,index) in recommends" :key="index">
     <a :href="item.link">
       <img :src="item.image" alt="">
       <div>{{item.title}}</div>
     </a>
   </div>
 </div>

</template>

<script>
export default{
  name:"recommendView",
  props:{
    recommends:{
      type:Array
    }
  }
}
</script>

<style scoped>
#recommendView{
  display: flex;
 
}
.recommend-item{
  flex:1;
  padding: 10px 15px 10px;
  text-align: center;
}
.recommend-item img{
  width: 70px;
  height: 70px;
}
</style>