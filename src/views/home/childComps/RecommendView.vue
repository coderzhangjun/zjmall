<template>
<div class="recommendview">
    <div v-for="(item,index) in recommends" :key="index" class="recmitem">
        <a :href="item.link">
        <img :src="item.image" alt="">
        <div>{{item.title}}</div>
    </a>
    </div>
</div>
</template>

<script>
export default {
  name: "RecommendView",
  props: {
    recommends: {
      type: Array,
      default: [],
    },
  },
};
</script>

<style scoped>
.recommendview{
    display: flex;
    margin-top: 10px;
    font-size: 14px;
    padding-bottom: 30px;
    border-bottom: 10px solid #eee;
}
.recmitem{
    flex: 1;
    text-align: center;
}
img {
    width: 80px;
    height: 80px;
    margin-bottom: 10px;
}

</style>