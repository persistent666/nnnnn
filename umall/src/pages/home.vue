<template>
  <div>
    <!-- 标签页 navBar -->
    <van-nav-bar title="首页" />
    <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
      <van-swipe-item v-for="item in bannerList" :key="item.id">
        <img :src="$preImg + item.img" alt="" />
      </van-swipe-item>
    </van-swipe>
    <van-tabs v-model="active">
      <van-tab title="热门推荐">
        <van-card
          v-for="item in goodsList[0].content"
          :key="item.id"
          tag="hot"
          :price="item.price"
          :title="item.goodsname"
          :thumb="$preImg + item.img"
        >
          <template #footer>
            <van-button type="primary" size="small" icon="cart-o"></van-button>
          </template>
        </van-card>
      </van-tab>
      <van-tab title="发现新品">
        <van-card
          v-for="item in goodsList[1].content"
          :key="item.id"
          tag="new"
          :price="item.price"
          :title="item.goodsname"
          :thumb="$preImg + item.img"
        >
          <template #footer>
            <van-button type="primary" size="small" icon="cart-o"></van-button>
          </template>
        </van-card>
      </van-tab>
      <van-tab title="全部商品">
        <van-card
          v-for="item in goodsList[2].content"
          :key="item.id"
          :price="item.price"
          :title="item.goodsname"
          :thumb="$preImg + item.img"
        >
          <template #footer>
            <van-button type="primary" size="small" icon="cart-o"></van-button>
          </template>
        </van-card>
      </van-tab>
    </van-tabs>
  </div>
</template>

<script>
import { getBanner, getIndexGoods } from "../utils/request";
export default {
  data() {
    return {
      active: 0,
      bannerList: [],
      goodsList: [{ content: [] }, { content: [] }, { content: [] }],
    };
  },
  methods: {
    requestBanner() {
      // 发起获取轮播图请求
      getBanner().then((res) => {
        this.bannerList = res.data.list;
      });
    },
    requestGoodsList() {
      getIndexGoods().then((res) => {
        this.goodsList = res.data.list;
      });
    },
  },
  mounted() {
    // 1.发起轮播图请求
    this.requestBanner();
    // 2.发起获取商品信息请求
    this.requestGoodsList();
  },
};
</script>

<style scoped>
.van-tab__pane {
  margin-bottom: 50px;
}
.my-swipe .van-swipe-item img {
  width: 100%;
  height: 100%;
}
</style>
