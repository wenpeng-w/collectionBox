<template>
  <div class="collection container">
    <div class="slideshow radius" @mouseover="clearInv" @mouseout="runInv">
      <transition-group tag="div" name="fade">
        <div v-show="nowIndex === index" v-for="(item, index) in hotSpots.hotItem" class="slide-img" :key="item">
          <a href="" class="pic" >
            <img :src="hotSpots.hotItem[index].image" alt="">
          </a>
          <div class="des">
            <span>{{ hotSpots.hotItem[index].description }}</span>
          </div>
        </div>
      </transition-group>
      <ul class="slide-pages">
      <li @click="toPages(prev)" class="page-btn">&lt;</li>
      <li :class="{ 'active': nowIndex === index }" @click="toPages(index)" v-for="(item, index) in hotSpots.hotItem">{{ index + 1 }}</li>
      <li @click="toPages(next)" class="page-btn">&gt;</li>
      </ul>
    </div>
    <div class="card">
      <div v-for="(card, index) in hotSpots.cards" class="card-item radius">
        <a :href="hotSpots.cards[index].cardUrl">
          <img :src="hotSpots.cards[index].cardImg" alt="">
        </a>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      hotSpots: {
        type: Object
      }
    },
    data () {
      return {
        nowIndex: 0,
        inv: 8000
      }
    },
    computed: {
      prev () {
        if (this.nowIndex === 0) {
          return this.hotSpots.hotItem.length - 1
        } else {
          return this.nowIndex - 1
        }
      },
      next () {
        if (this.nowIndex === this.hotSpots.hotItem.length - 1) {
          return 0
        } else {
          return this.nowIndex + 1
        }
      }
    },
    methods: {
      toPages (index) {
        this.nowIndex = index
      },
      runInv () {
        this.invTimer = setInterval(() => {
          this.toPages(this.next)
        }, this.inv)
      },
      clearInv () {
        clearInterval(this.invTimer)
      }
    },
    mounted () {
      this.runInv()
    }
  }
</script>

<style lang="less" rel="stylesheet/less" scoped>
@import url("../common/less/index.less");

.collection {
  .slideshow {
    position: relative;
    width: 100%;
    padding-top: 31.25%;
    .slide-img {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      .pic {
        display: block;
        img {
          width: 100%;
          vertical-align: top;
        }
      }
      .des {
        position: absolute;
        bottom: 15px;
        left: 0;
        width: 100%;
        height: 40px;
        line-height: 40px;
        color: #fff;
        font-size: 14px;
        span {
          display: block;
          padding: 0 15px;
          margin: 0 30px;
          background-color: rgba(0, 0, 0, 0.4);
          border-radius: 20px;
          overflow: hidden;
        }
      }
    }
    .fade-enter-active, .fade-leave-active {
      transition: all 1s;
    }
    .fade-enter, .fade-leave-active {
      opacity: 0;
    }
    .slide-pages {
      position: absolute;
      bottom: 25px;
      right: 40px;
      li {
        float: left;
        width: 20px;
        height: 20px;
        line-height: 20px;
        margin: 0 4px;
        background-color: rgba(255, 255, 255, 0.2);
        border-radius: 50%;
        font-size: 12px;
        color: #ffffff;
        text-align: center;
        cursor: pointer;
      }
      .active {
        color: #ffffff;
        background-color: #24292e;
      }
      .page-btn {
        background-color: rgba(255, 255, 255, 0.4);
      }
    }
  }
  .card {
    width: 100%;
    overflow: hidden;
    margin-top: 15px;
    .card-item {
      float: left;
      width: 24%;
      margin-right: 1.333334%;
      background-color: #f5f5f5;
      &:last-child {
        margin-right: 0;
      }
      img {
        width: 100%;
        vertical-align: top;
      }
    }
  }
}
</style>
