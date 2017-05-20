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
    <div class="main">
      <div class="article">
        <ul class="article-list">
          <li v-for="(item, index) in hotSpots.articleList" :class="{'have-pic': item.artPic}">
            <div class="content">
              <h2 class="title">{{ item.artTitle }}</h2>
              <p class="description">{{ item.artDesc }}</p>
              <div class="tag">
                <span class="tag-a" v-for="tag in item.artTag">{{ tag }}</span>
              </div>
            </div>
            <div v-show="item.artPic" class="pic">
              <img :src="item.artPic" alt="">
            </div>
          </li>
        </ul>
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
    margin-bottom: 40px;
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
    margin-bottom: 40px;
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
  .main {
    .article {
      width: 70%;
      padding-top: 16px;
      border-top: 1px solid #f0f0f0;
      .article-list {
        li {
          position: relative;
          margin: 0 0 16px;
          padding: 0 2px 16px 0;
          border-bottom: 1px solid #f0f0f0;
          word-wrap: break-word;
          .content {
            .title {
              margin-bottom: 4px;
              font-size: 16px;
              font-weight: 700;
              line-height: 1.5;
            }
            .description {
              margin: 0 0 8px;
              font-size: 14px;
              line-height: 24px;
            }
            .tag {
              font-size: 12px;
              .tag-a {
                display: inline-block;
                padding: 2px 6px;
                margin-right: 10px;
                color: rgb(102, 172, 172);
                border: 1px solid rgb(102, 172, 172, 0.8);
                border-radius: 3px;
              }
            }
          }
          .pic {
            position: absolute;
            top: 50%;
            margin-top: -69px;
            right: 2px;
            width: 150px;
            height: 120px;
            img {
              width: 100%;
              height: 100%;
              border-radius: 4px;
              border: 1px solid #f0f0f0;
              vertical-align: top;
            }
          }
        }
        .have-pic {
          .content {
            padding-right: 160px;
          }
        }
      }
    }
  }
}
</style>
