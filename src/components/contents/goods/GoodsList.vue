<template>
  <div id="goods-list" >
   <goods-list-item v-for="(item,index) in goodsdata" :key="index" :goodsItem="item">
    
   </goods-list-item>
  </div>
</template>

<script>
import GoodsListItem from "./GoodsListItem"
export default{
  name:"GoodsList",
  components:{
    GoodsListItem 
  },
  props:{
    goodsdata:{
      type:Array,
      default(){
        return []
      }
    }
  }
}
</script>

<style scoped>
#goods-list{
  margin-top: 20px;

  display: flex;
  flex-wrap: wrap;
}

</style>