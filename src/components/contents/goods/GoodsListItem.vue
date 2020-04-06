<template>
  <div id="goods-list-item"  >
    <img :src="goodsItem.show.img" alt="" @load="loadSucess" @click="itemClick">
    <div class="info">
      <p>{{goodsItem.title}}</p>
      <span class="price">${{goodsItem.price}}</span>
      <span class="cfav">{{goodsItem.cfav}}</span>   
    </div>
 
  </div>
</template>

<script>
export default{
  name:"GoodsListItem",
  props:{
    goodsItem:{
      type:Object,
      default(){
        return {}
      }
    }
  },
  methods:{
   loadSucess(){
     this.$bus.$emit("imageLoad")
   },
   itemClick(){
     this.$router.push({
       path:"/detail",
       query:{
         iid:this.goodsItem.iid
       }
     })
    // this.$router.push("/detail/"+this.goodsItem.iid)
   }
  }
}
</script>

<style scoped>
#goods-list-item {
  position: relative;
  padding: 5px 5px 40px;
  width: 50%;

} 
#goods-list-item img{
  width: 100%; 
}
#goods-list-item .info{
  position: absolute;
  bottom: 5px;
  left: 0;
  right: 0;

  text-align: center;
}
.info p{
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
.info .price{
  position:relative;
}
.info .price::after{  

  position:absolute;
  top: 1px;
  right: -15px;
  content:"";
  background:url("~assets/img/common/collect.svg")  no-repeat ;
  background-size: 100%;
  width: 14px;
  height: 14px;
}
.info .cfav{
  margin-left: 15px;
}
</style>