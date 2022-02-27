<template>
  <div class="home">
    <nav-bar class="nav-bar">
      <div slot="center">购物街</div>
    </nav-bar>
    <back-top v-show="isshow" ></back-top>
    <div id="ceshi">
      <home-swiper :banners="banners" ref="hSwiper"></home-swiper>
    </div>
    <recommend-view :recommends="recommends"></recommend-view>
    <feature-view></feature-view>
    <tab-control
      :titles="['流行', '新款', '精选']"
      @tabclick="tabclick"
    ></tab-control>
    <goods-list :goods="goods[currentType].list"></goods-list>
  </div>
</template>

<script>
import NavBar from "../../components/common/navbar/NavBar.vue";
import HomeSwiper from "./childComps/HomeSwiper.vue";
import RecommendView from "./childComps/RecommendView.vue";
import FeatureView from "./childComps/FeatureView.vue";
import TabControl from "../../components/content/tabControl/TabControl";
import GoodsList from "../../components/content/goods/GoodsList.vue";
import BackTop from "content/backTop/BackTop"

import {
  getHomeMultidata,
  getHomeData,
  getHomeGoods,
  RECOMMEND,
  BANNER,
} from "network/home";
export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
    GoodsList,
    BackTop
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] },
      },
      currentType:'pop',
      isshow:"false"
    };
  },
mounted(){
    document.addEventListener('scroll',function(){  
      console.log(window.pageYOffset);
      this.isshow = window.pageYOffset >1000
    })

  },
  created() {
    this.getHomeMultidata(), 
    this.getHomeGoods('pop'),
    this.getHomeGoods('new'),
    this.getHomeGoods('sell');
  },
  methods: {
     backshow(){ },

/*数据请求*/
tabclick(index){
switch(index){
  case 0:
  this.currentType = 'pop'
  break
  case 1:
  this.currentType = 'new'
  break
  case 2:
  this.currentType = 'sell'
  break


}
},

    /*网络请求*/
    getHomeMultidata() {
      getHomeMultidata().then((res) => {
        console.log(res);
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
        console.log(this.recommends);
      });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1
      getHomeGoods(type, page).then((res) => {
        console.log(res);
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
      });
    },
  },
  activated: function () {
    this.$refs.hSwiper.startTimer();
  },
  deactivated: function () {
    this.$refs.hSwiper.stopTimer();
  },
};
</script>

<style scoped>
#home {
  height: 100vh;
}

.nav-bar {
  background-color: #ff8198;
  font-weight: 700;
  color: #fff;
  position: sticky;
  top: 0px;
}
</style>

