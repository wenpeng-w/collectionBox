<template>
  <div class="collection container">
    <div class="slideshow">
      <ul>
        <li v-for="(item, index) in hotSpots.hotItem" class="slide-item">
          <img class="pic" :src="hotSpots.hotItem[index].image" alt="">
          <p class="des">{{ hotSpots.hotItem[index].description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      hotSpots: {
        type: Object
      }
    }
  }
</script>

<style lang="less" rel="stylesheet/less" scoped>
@import url("../common/less/index.less");

.collection {
  position: relative;
  .slideshow {
    .slide-item {
      position: absolute;
      left: 0;
      top: 0;
      .pic {
        width: 100%;
        vertical-align: top;
      }
      .des {
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 40px;
        line-height: 40px;
        background-color: rgba(0, 0, 0, 0.4);
        text-indent: 15px;
        color: #fff;
      }
    }
  }
}
</style>
