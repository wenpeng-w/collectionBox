<template>
  <div class="go-top">
    <a @click="goTop" href="javascript:void(0);" class="content">↑</a>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  methods: {
    goTop () {
      document.documentElement.scrollTop = document.body.scrollTop = 0
    }
  }
}
</script>

<style lang="less" rel="stylesheet/less" scoped>
  .go-top {
    position: fixed;
    right: 40px;
    bottom: 40px;
    .content {
      display: block;
      width: 40px;
      height: 40px;
      line-height: 40px;
      border: 1px solid #cecece;
      border-radius: 4px;
      cursor: pointer;
      font-size: 16px;
      text-align: center;
      color: #aeaeae;
      &:hover {
        background-color: #f5f5f5;
      }
    }
  }
</style>
