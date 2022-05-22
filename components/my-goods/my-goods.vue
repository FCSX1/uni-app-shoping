<template>
  <view class="goods-item">
    <!-- 左侧的盒子 -->
    <view class="goods-item-left">

      <radio :checked="goods.goods_state" color="#c00000" v-if="showRadio" @click="radioClickHandler"></radio>

      <image :src="goods.goods_small_logo || defaultPic" class="goods-pic"></image>
    </view>
    <!-- 右侧的盒子 -->
    <view class="goods-item-right">
      <view class="goods-name">
        <!-- 商品的名字 -->
        {{goods.goods_name}}
      </view>
      <view class="goods-info-box">
        <view class="goods-price">
          ￥{{this.goods.goods_price | tofixed}}
        </view>
        <uni-number-box :min="1" :value="goods.goods_count" v-if="showNum" @change="numChangeHandler"></uni-number-box>
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    props: {
      goods: {
        type: Object,
        required: true
      },
      showRadio: {
        type: Boolean,
        // 默认情况下，不会展示 radio 组件
        default: false
      },
      showNum: {
        type: Boolean,
        default: false
      }
    },
    name: "my-goods",
    data() {
      return {
        // 默认图片
        defaultPic: 'https://img3.doubanio.com/f/movie/8dd0c794499fe925ae2ae89ee30cd225750457b4/pics/movie/celebrity-default-medium.png'
      }
    },
    filters: {
      tofixed(num) {
        return Number(num).toFixed(2)
      }
    },
    methods: {
      // 这是 radio 组件的 点击事件处理函数
      radioClickHandler() {
        this.$emit('radio-change', {
          goods_id: this.goods.goods_id,
          goods_state: !this.goods.goods_state
        })
      },
      // 监听到了 NumberBox 组件数量变化的事件
      numChangeHandler(val) {
        this.$emit('num-change', {
          goods_id: this.goods.goods_id,
          goods_count: val - 0
        })
        console.log(val);
      }
    }
  }
</script>

<style lang="scss">
  .goods-item {
    // 让 goods-item 项占满整个屏幕的宽度
    width: 750rpx;
    // 设置盒模型为 border-box
    box-sizing: border-box;
    display: flex;
    padding: 10px 5px;
    border-bottom: 1px solid #f0f0f0;

    .goods-item-left {
      margin-right: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;

      .goods-pic {
        width: 100px;
        height: 100px;
        display: block;
      }
    }

    .goods-item-right {
      display: flex;
      flex: 1;
      flex-direction: column;
      justify-content: space-between;

      .goods-name {
        font-size: 13px;
      }

      .goods-info-box {
        display: flex;
        justify-content: space-between;
        align-items: center;

        .goods-price {
          color: #c00000;
          font-size: 16px;
        }
      }
    }
  }
</style>
