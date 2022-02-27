<template>
  <div class="back-top" @click="backclick">
    <img src="../../../assets/img/common/top.png" alt="" />
  </div>
</template>

<script>
export default {
  name: "BackTop",
  methods:{
      backclick(){
         
           window.scrollTo(0, 0,5000)
      }
  }
};
</script>

<style scoped>
.back-top {
  position: fixed;

  right: 10px;
  bottom: 60px;
  z-index: 10;
}
.back-top img{
    width: 150px;
    height: 150px;
}
</style>