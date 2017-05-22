<template>
  <div class="collection container">
    <div class="slideshow radius" @mouseover="clearInv" @mouseout="runInv">
      <transition-group tag="div" name="fade">
        <div v-show="nowIndex === index" v-for="(item, index) in hotSpots.hotItem" class="slide-img" :key="item">
          <a href="" class="pic">
            <img :src="hotSpots.hotItem[index].image" alt="">
          </a>
          <div class="des">
            <span>{{ hotSpots.hotItem[index].description }}</span>
          </div>
        </div>
      </transition-group>
      <ul class="slide-pages">
        <li @click="toPages(prev)" class="page-btn">&lt;</li>
        <li :class="{ 'active': nowIndex === index }" @click="toPages(index)" v-for="(item, index) in hotSpots.hotItem">
          {{ index + 1 }}
        </li>
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
              <div class="author">
                <img class="avator" :src="item.avator" alt="">
                <span class="name">{{ item.name }}</span>
                <span class="time">{{ item.time | formatDate }}</span>
              </div>
              <h2 class="title"><a :href="item.artUrl">{{ item.artTitle }}</a></h2>
              <p class="description">{{ item.artDesc }}</p>
              <div class="tag">
                <span :class="'tag-c_' + index" v-for="(tag, index) in item.artTag" class="tag-a">{{ tag }}</span>
              </div>
            </div>
            <div v-if="item.artPic" class="pic">
              <a :href="item.artUrl"><img :src="item.artPic" alt=""></a>
            </div>
          </li>
        </ul>
        <div class="page-number">
          <a href="javascript:void(0);" class="num prev-page">←</a><a v-for="(page, index) in 5" href="javascript:void(0);" class="num">{{ index + 1 }}</a><a href="javascript:void(0);" class="num prev-page">→</a>
        </div>
      </div>
      <div class="sidebar">
        <div class="contact radius">
          <div class="bg-img">
            <img src="../common/images/tooopen_sy_130972012989.jpg">
          </div>
          <div class="way">
            <a href="" class="way-link github">
              <i class="iconfont"></i><span>github</span>
            </a>
            <a href="" class="way-link sina">
              <i class="iconfont"></i><span>新浪</span>
            </a>
            <a href="" class="way-link jianshu">
              <i class="iconfont"></i><span>简书</span>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import {formatDate} from '../common/js/date'

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
    },
    filters: {
      formatDate (time) {
        // 获取当天凌晨的时间戳
        let nowDate = new Date().setHours(0, 0, 0, 0)
        let nowYear = new Date().getFullYear()
        let date = new Date(time)

        let daysDiff = (nowDate - date) / 86400000
        let yearsDiff = nowYear - date.getFullYear()

        if (daysDiff < 0) {
          return formatDate(date, '今天 hh:mm')
        } else if (daysDiff < 1) {
          return formatDate(date, '昨天 hh:mm')
        } else if (daysDiff < 2) {
          return formatDate(date, '前天 hh:mm')
        } else if (yearsDiff > 0) {
          return formatDate(date, 'yyyy.MM.dd hh:mm')
        } else {
          return formatDate(date, 'MM.dd hh:mm')
        }
      }
    }
  }
</script>

<style lang="less" rel="stylesheet/less" scoped>
  @import url("../common/less/index.less");

  @tagColor_0: rgb(102, 172, 172);
  @tagColor_1: rgb(253, 96, 95);
  @tagColor_2: rgb(65, 184, 131);
  @tagColor_3: rgb(255, 47, 139);
  @tagAlpha: 0.6;
  .border-color (@tagColor, @tagAlpha) {
    border-color: rgba(@tagColor, @tagAlpha);
  };

  .collection {
    padding-top: 70px;
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
      position: relative;
      width: 100%;
      overflow: hidden;
      .article {
        float: left;
        width: 66%;
        padding-top: 16px;
        border-top: 1px solid #f0f0f0;
        .article-list {
          margin-bottom: 30px;
          li {
            position: relative;
            margin: 0 0 16px;
            padding: 0 2px 16px 0;
            border-bottom: 1px solid #f0f0f0;
            word-wrap: break-word;
            .content {
              .author {
                margin-bottom: 6px;
                font-size: 14px;
                .avator {
                  width: 26px;
                  height: 26px;
                  border: 1px solid #ccc;
                  border-radius: 50%;
                  overflow: hidden;
                  margin-right: 6px;
                  vertical-align: middle;
                }
                .name {
                  vertical-align: middle;
                  margin-right: 6px;
                  color: #767676;
                }
                .time {
                  vertical-align: middle;
                  color: #969696;
                }
              }
              .title {
                a {
                  display: block;
                  margin-bottom: 4px;
                  font-size: 16px;
                  font-weight: 700;
                  line-height: 1.5;
                  color: rgba(0, 0, 0, 0.75);
                  &:hover {
                    text-decoration: underline;
                  }
                }
              }
              .description {
                margin: 0 0 8px;
                font-size: 14px;
                line-height: 24px;
                color: rgba(0, 0, 0, 0.6);
              }
              .tag {
                font-size: 12px;
                line-height: 15px;
                .tag-a {
                  display: inline-block;
                  padding: 2px 6px;
                  margin-right: 10px;
                  border-radius: 3px;
                  border-width: 1px;
                  border-style: solid;
                }
                .tag-c_0 {
                  color: @tagColor_0;
                  border-color: lighten(@tagColor_0, @tagAlpha);
                }
                .tag-c_1 {
                  color: @tagColor_1;
                  border-color: lighten(@tagColor_1, @tagAlpha);
                }
                .tag-c_2 {
                  color: @tagColor_2;
                  border-color: lighten(@tagColor_2, @tagAlpha);
                }
                .tag-c_3 {
                  color: @tagColor_3;
                  border-color: lighten(@tagColor_3, @tagAlpha);
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
        .page-number {
          margin-bottom: 40px;
          text-align: center;
          .num {
            display: inline-block;
            width: 28px;
            height: 28px;
            line-height: 28px;
            margin: 0 4px;
            border: 1px solid rgba(102, 172, 172, 0.8);
            border-radius: 4px;
            text-align: center;
            font-size: 13px;
            transition: all 0.2s;
            &:hover {
              background-color: rgba(102, 172, 172, 0.6);
              border-radius: 50%;
              color: #ffffff;
            }
          }
        }
      }
      .sidebar {
        float: left;
        width: 29.8334%;
        margin-left: 4.1667%;
        .contact {
          position: relative;
          margin-bottom: 30px;
          border: 1px solid #f0f0f0;
          .bg-img {
            width: 100%;
            img {
              width: 100%;
              vertical-align: top;
            }
          }
          .way {
            position: absolute;
            left: 0;
            right: 0;
            bottom: 10px;
            padding: 4px 8px;
            text-align: center;
            .way-link {
              display: inline-block;
              width: 26%;
              margin: 0 4px;
              padding: 2px;
              line-height: 30px;
              border-radius: 4px;
              font-size: 14px;
              color: #fff;
              text-align: center;
              transition: all 0.2s;
              .iconfont {
                margin-right: 4px;
              }
            }
            .github {
              background-color: rgba(43, 41, 46, 1);
              &:hover {
                background-color: rgba(43, 41, 46, 0.9);
              }
            }
            .sina {
              background-color: rgba(255, 129, 64, 1);
              &:hover {
                background-color: rgba(255, 129, 64, 0.9);
              }
            }
            .jianshu {
              background-color: rgba(243, 115, 93, 1);
              &:hover {
                background-color: rgba(243, 115, 93, 0.9);
              }
            }
          }
        }
      }
    }
  }
</style>
