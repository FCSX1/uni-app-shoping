<template>
  <view>
    <view class="cart-container" v-if="cart.length !== 0">
      <!-- 收货地址组件 -->
      <my-address></my-address>
      <!-- 商品列表的标题区域 -->
      <view class="cart-title">
        <!-- 左侧的图标 -->
        <uni-icons type="shop" size="18"></uni-icons>
        <!-- 右侧的文本 -->
        <text class="cart-title-text">购物车</text>
      </view>

      <!-- 循环渲染购物扯中的商品信息 -->
      <!-- 商品列表区域 -->
      <!-- uni-swipe-action 是最外层包裹性质的容器 -->
      <uni-swipe-action>
        <block v-for="(goods, i) in cart" :key="i">
          <!-- uni-swipe-action-item 可以为其子节点提供滑动操作的效果。需要通过 options 属性来指定操作按钮的配置信息 -->
          <uni-swipe-action-item :right-options="options">
            <my-goods :goods=" goods" :show-radio="true" :show-num="true" @radio-change="radioChangeHandler"
              @num-change="numberChangeHandler">
            </my-goods>

            <template v-slot:right>

              <view class="slot-button" @click="swipeActionClickHandler(goods)">

                <text class="slot-button-text">删除</text>

              </view>

            </template>
          </uni-swipe-action-item>
        </block>
      </uni-swipe-action>

      <!-- 使用自定义的结算组件 -->
      <my-settle class="my-settle-container"></my-settle>
    </view>

    <!-- 空白购物车的区域 -->
    <view class="empty-cart" v-else>
      <image src="/static/cart_empty@2x.png" class="empty-img"></image>
      <text class="tip-text">空空如也~</text>
    </view>


  </view>
</template>

<script>
  import badgeMix from '@/mixins/tabber-badge.js';
  import {
    mapState,
    mapMutations
  } from 'vuex'
  export default {
    mixins: [badgeMix],
    computed: {
      ...mapState('m_cart', ['cart'])
    },
    data() {
      return {
        options: [{
          text: '删除',
          style: {
            backgroundColor: '#c00000'
          }
        }]
      }
    },
    methods: {
      ...mapMutations('m_cart', ['updateGoodsState', 'updateGoodsCount', 'removeGoodsById']),
      radioChangeHandler(e) {
        this.updateGoodsState(e)
      },
      numberChangeHandler(e) {
        this.updateGoodsCount(e)
      },
      // 点击了滑动操作按钮
      swipeActionClickHandler(goods) {
        this.removeGoodsById(goods.goods_id)
      }
    }
  }
</script>

<style lang="scss">
  .cart-container {
    padding-bottom: 50px;
  }

  .cart-title {
    height: 40px;
    display: flex;
    align-items: center;
    padding-left: 5px;
    border-bottom: 1px solid #efefef;

    .cart-title-text {
      font-size: 14px;
      margin-left: 10px;
    }
  }

  .slot-button-text {
    color: #f0f0f0;
    font-size: 14px;

  }

  .slot-button {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #C00000;
    width: 120rpx;
  }

  .empty-cart {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 150px;

    .empty-img {
      width: 90px;
      height: 90px;
    }

    .tip-text {
      font-size: 12px;
      color: gray;
      margin-top: 15px;
    }
  }
</style>
