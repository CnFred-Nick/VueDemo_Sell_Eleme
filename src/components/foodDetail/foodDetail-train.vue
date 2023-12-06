<template>
  <transition name="move">
    <div class="detailWrapper" ref="detailWrapper" v-show="showDetail">
      <div class="foodDetail">
        <div class="back" @click="showToggle()">
          <i class="icon-arrow_lift"></i>
        </div>
        <img :src="food.image" height="425" width="100%">
        <div class="info">
            <div class="title">{{food.name}}</div>
          <div class="desc">
              <span>月售{{food.sellCount}}</span>
            <span>好评率{{food.rating}}%</span>
          </div>
        </div>
        <div class="price">
          <span class="unit">￥</span>{{food.price}}
          <span class="oldPrice" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
        </div>
        <div class = "shopCart">
          <transition name = "fade">
            <div class="text" @click="addCart($event)" v-show="!food.count">加入购物车</div>
          </transition>
        </div>
        <cartcontrol-train :food="food"></cartcontrol-train>
      </div>
    </div>
    <div class="divider"></div>
    <div class="desc">
        <div class="title">商品介绍</div>
      <div class="content">{{food.info}}</div>
    </div>
    <div class="divider"></div>
    <div class="evalution">
      <div class = 'title'>商品评价</div>
      <div class="classify">
        <span v-for=""></span>
      </div>
    </div>
  </transition>
</template>

<script>

import Cartcontrol from "../cartcontrol/cartcontrol";
import CartcontrolTrain from "../cartcontrol/cartcontrol-train";
export default {
  components: {CartcontrolTrain, Cartcontrol},
  props: {
    food: Object
  },
  data() {
    return {
      showDetail: false
    }
  },
  methods: {
    showToggle() {
      this.showDetail = !this.showDetail;
      if (this.showDetail) {
        this.$nextTick(() => {
          this._initScroll()
        })
      }
    },
    _initScroll() {
      if (!this.detailWrapper) {
        this.detailWrapper = new BScroll(this.$refs.detailWrapper, {
          click: true
        });
      } else {
        this.detailWrapper.refresh()
      }
    },

  }
}
</script>