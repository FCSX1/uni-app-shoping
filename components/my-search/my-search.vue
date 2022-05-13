<template>
  <view class="my-search-container" :style="{'background-color':bgcolor}" @click="searchBoxHandler">
    <view class="my-search-box" :style="{'border-radius':radius + 'px'}">
      <!-- 使用 uni-ui 提供的图标组件 -->
      <uni-icons type="search" size="16"></uni-icons>
      <text class="placeholder">搜索</text>
    </view>
  </view>
</template>

<script>
  export default {
    props: {
      // 背景颜色
      bgcolor: {
        type: String,
        default: '#007aff'
      },
      // 边框圆角
      radius: {
        type: Number,
        // 单位 px
        default: 18
      }
    },
    name: "my-search",
    data() {
      return {

      }
    },
    methods: {
      searchBoxHandler() {
        this.$emit('click')
      }
    }
  }
</script>

<style lang="scss">
  .my-search-container {
    height: 50px;
    // background-color: #007aff;
    padding: 0 10px;
    display: flex;
    align-items: center;


    .my-search-box {
      height: 36px;
      background-color: #fff;
      // border-radius: 15px;
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: center;

      .placeholder {
        font-size: 15px;
        margin-left: 5px;
      }
    }
  }
</style>
