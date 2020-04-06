<template>
  <div id="tab-control">
    <div class="control-item" v-for="(item,index) in title" :key="item.id"  >
      <span :class="{'active':currentIndex==index}" @click="tabClick(index)">{{item}}</span>
    </div>   
  </div>
</template>

<script>
export default{
  name:"TabControl",
  props:{
    title:{
      type:Array,
      default(){
        return[]
      }
    }
  },
  data(){
    return {
      currentIndex:0
    }
  },
  methods:{
    tabClick(index){
      this.currentIndex=index;
      this.$emit("itemClick",index)
    }
  }
}
</script>

<style scoped>
#tab-control{
  
  /* position: sticky;
  z-index: 1;
  top: 44px; */
  display: flex;
  padding-bottom: 10px;
  background-color: var(--color-background);
}
.control-item{
  flex: 1;
  text-align: center;
}
.control-item span{
  border-bottom:3px solid var(--color-tint);  
  padding-bottom: 5px;
}
.active{
  color: red;
}
</style>