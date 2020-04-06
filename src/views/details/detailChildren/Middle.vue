<template>
  <div>
    <div class="title">{{goods.title}}</div>
    <div class="price">
      <span>{{goods.newPrice}}</span>
      <span>{{goods.oldPrice}}</span>
      <span>{{goods.discount}}</span>
    </div> 
    <div class="hot">
      <span v-if="goods.columns">{{goods.columns[0]}}</span>
      <span v-if="goods.columns">{{goods.columns[1]}}</span>
      <span v-if="goods.services"> {{goods.services[3].name}}</span>
    </div>
    <div class="post" v-if="goods.services">
      <span>{{goods.services[0].name}}</span>
      <span>{{goods.services[1].name}}</span>
      <span>{{goods.services[2].name}}</span>
    </div>
    <div class="store">
       <div class="logo">
         <img :src="shop.logo" alt="">
         <span>{{shop.name}}</span>
       </div>
       <div>
         <div><span>{{shop.fans}}</span></div>
         <div>{{shop.sells}}</div>
         <div v-if="shop.score">{{shop.score[0]}}</div>
         <div>{{}}</div>
       </div>
    </div>
     <span>{{goods.desc}}</span>
      <span>{{goodsparam.infos}}</span> 
  </div>
</template>
<script>
export default{ 
  name:'Middle',
  props:{
    goods:{
      type:Object,
      default(){
        return {}
      }
    },
    goodsparam:{},
    shop:{
      type:Object,
      default(){
        return {}
      }
    }
  }
}
</script>


<style scoped>
.title{
  color: black;
  margin-bottom: 10px;
}
.price{
  margin-bottom: 10px;
}
.price :nth-child(1){
  color: deeppink;
  margin-left: 10px;
  margin-right: 5px;
}
.price :nth-child(2){
  color: grey;
  font-size: 12px;
  margin-right: 5px;
}
.price :nth-child(3){
  color:white;
  border-radius: 5px;
  font-size: 12px;
  background-color: deeppink;
}
.hot{
  position: relative;
  color: grey;
  font-size: 12px;
}
.hot :nth-child(1){
  position: absolute;
  left: 10px;
  
  
}
.hot :nth-child(2){
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}
.hot :nth-child(3){
  position: absolute;
  right: 10px;
}

.post{
  margin-top: 30px;
  border-top: 1px solid grey;
  border-bottom: 1px solid grey;
  padding: 15px 0 15px;
  display: flex;
  text-align: center;
}
.post span{
  flex: 1;
}

.logo {
  display: flex;
  align-items:center; 
  height: 100px;
}
.logo img{
  height: 100%;
}
.logo span{
  flex:1;
  /* align-self: center; */
  
}
</style>