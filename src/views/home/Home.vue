<template>
  <div id="home">
    <nav-bar class="home-nav">
      <span slot="center">购物街</span>
    </nav-bar>
    <home-swiper :banners="banners"></home-swiper>
    <recommend-view :recommends="recommends"></recommend-view>
    <feature-view></feature-view>
    <tab-control :titles="['流行', '新款', '精选']" @tabClick="tabClick"></tab-control>
    <keep-alive>
      <div class="goodList">
        <!-- <span v-text="goods[itemindex]" ></span> -->
        <div class="goods">
          <div
            v-for="item in goodsimg[goodsindex]"
            :key="item.iid"
            @click="goodsClick(item.iid)"
            link="/detail"
            class="goodsItem"
          >
            <img :src="item.imgurl" :alt="item.imgsub" />
            <p>{{item.imgsub}}</p>
          </div>
        </div>
      </div>
    </keep-alive>
  </div>
</template>

<script>
import NavBar from "common/navbar/NavBar";
import HomeSwiper from "./childComps/HomeSwiper";
import RecommendView from "@/views/home/childComps/RecommendView";
import FeatureView from "@/views/home/childComps/FeatureView";

import TabControl from "@/components/content/tabControl/TabControl";

import { getHomeMultidata } from "network/Home";
// import func from '../../../vue-temp/vue-editor-bridge'

export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
  },

  data() {
    return {
      banners: [],
      recommends: [],
      goods: ["流行", "新款", "精选"],
      goodsimg: [
        [
          {
            imgurl: require("../../assets/img/home/goods1.webp"),
            imgsub: "流行",
            iid: 1,
          },
          {
            imgurl: require("../../assets/img/home/goods2.webp"),
            imgsub: "满意",
            iid: 2,
          },
          {
            imgurl: require("../../assets/img/home/goods3.webp"),
            imgsub: "新款",
            iid: 3,
          },
          {
            imgurl: require("../../assets/img/home/goods4.webp"),
            imgsub: "满意",
            iid: 4,
          },
          {
            imgurl: require("../../assets/img/home/goods5.webp"),
            imgsub: "精选",
            iid: 5,
          },
          {
            imgurl: require("../../assets/img/home/goods6.webp"),
            imgsub: "满意",
            iid: 6,
          },
          {
            imgurl: require("../../assets/img/home/goods1.webp"),
            imgsub: "流行",
            iid: 7,
          },
          {
            imgurl: require("../../assets/img/home/goods2.webp"),
            imgsub: "满意",
            iid: 8,
          },
        ],
        [
          {
            imgurl: require("../../assets/img/home/goods3.webp"),
            imgsub: "新款",
            iid: 9,
          },
          {
            imgurl: require("../../assets/img/home/goods4.webp"),
            imgsub: "满意",
            iid: 10,
          },
        ],
        [
          {
            imgurl: require("../../assets/img/home/goods5.webp"),
            imgsub: "精选",
            iid: 11,
          },
          {
            imgurl: require("../../assets/img/home/goods6.webp"),
            imgsub: "满意",
            iid: 12,
          },
        ],
      ],
      itemindex: 0,
      goodsindex: 0,
    };
  },
  created() {
    const that = this
    getHomeMultidata()
      .then((res) => {
        that.banners = res.data.banner;
        that.recommends = res.data.recommend;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    tabClick(index) {
      // console.log(index);
      this.itemindex = index;
      this.goodsindex = index;
    },
    goodsClick(iid) {
      this.$router.push({ path: "/detail/" + iid });
      console.log(this.goodsimg);
      for(let i = 0; i < this.goodsimg.length; i ++) {
        for (let j = 0; j < this.goodsimg[i].length; j ++) {
          if (this.goodsimg[i][j]["iid"] == iid) {
            this.$store.commit("changeCurrentGoodInfo", { currentGoodInfo: this.goodsimg[i][j] })
            return
          }
        }
      }
    },
  },
};
</script>

<style scoped>
#home {
  padding-top: 44px;
}
.home-nav {
  background-color: var(--color-tint);
  color: #ffffff;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
}
.goodList {
  /* height: 150vh; */
  margin-bottom: 49px;
}
.goods {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  height: 100%;
  font-size: 14px;
  border-bottom: 10px solid #eee;
}
.goodsItem {
  flex: 1;

  text-align: center;
  flex: 0 0 50%;
}
.goodsItem > img {
  width: 100%;
  /* height: 50%; */
}
</style>
