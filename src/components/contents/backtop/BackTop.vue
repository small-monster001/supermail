<template>
  <div class="backtop">
    <img src="~assets/img/common/top.png"> 
  </div>
</template>

<script>
export default{
  name:'BackTop'
}
</script>

<style scoped>
.backtop{
  width: 43px;
  height: 43px;
  /* 不知道为什么用绝对定位会出bug */
  position: fixed;
  bottom: 49px;
  right: 5px;

}
.backtop img{
  width: 100%;
  height: 100%;
}
</style>