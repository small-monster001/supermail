<template>
   <div id="tabBarItem" @click="itemClick">
     <slot v-if="isActive" name="item-icon"></slot>
     <slot v-else name="item-icon-active"></slot>
     <div :style="color"><slot name="item-text"></slot></div>
   </div>
</template>

<script>
  export default{
    name:"TabBarItem",
    data(){
      return {
        
      }
    },
    props:{
      path:String,
      abc:{
        type:String,
        default:"blue"
      }
    },
    methods:{
      itemClick(){
       this.$router.replace(this.path);
           
      }
    },
    computed:{
      isActive(){
        return  this.$route.path.indexOf(this.path)==-1
        // return this.$route.path!==this.path
      },
      color(){
        return this.isActive?{}:{color:this.abc}
      }
    }
  }
</script>

<style scoped>
#tabBarItem img{
  width:22px;
  height:22px;
  vertical-align: middle;
  margin:3px 0 2px;
}
#tabBarItem{
  flex:1;
  text-align:center;
  height: 49px;
}

</style>