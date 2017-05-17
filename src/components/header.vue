<template>
  <div class="header">
    <a class="logo" href="/"><img height="44" src="../common/images/0l6l1y8b.png" alt="0618"></a>
    <div class="tool-bar">
      <a href="https://github.com/wenpeng-w" class="tool-item">GitHub</a>
    </div>
    <div class="container">
      <ul class="nav">
        <li class="nav-item"><router-link to="/collection">首页</router-link></li>
        <li class="nav-item"><router-link to="/home">规范</router-link></li>
        <li class="nav-item"><router-link to="/home">H5</router-link></li>
        <li class="nav-item"><router-link to="/home">主页</router-link></li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" rel="stylesheet/less" scoped>
  @import url("../common/less/index.less");

  .header {
    position: relative;
    width: 100%;
    height: 70px;
    margin-bottom: 15px;
    background: #ffffff;
    border-bottom: 1px solid #f0f0f0;
    overflow: hidden;
  }
  .logo {
    float: left;
    height: 44px;
    padding: 8px 10px;
    margin-top: 5px;
  }
  .tool-bar {
    float: right;
    .tool-item {
      display: block;
      height: 26px;
      line-height: 26px;
      padding: 0 10px;
      margin: 21px 20px 0 0;
      border: 1px solid #24292e;
      border-radius: 2px;
      color: #24292e;
      &:hover {
        color: #ffffff;
        background-color: #24292e;
      }
    }
  }
  .nav {
    margin-top: 15px;
    height: 40px;
    line-height: 40px;
    .nav-item {
      float: left;
      margin: 0 12px;
      a {
        display: block;
        width: 40px;
        height: 40px;
        background-color: rgba(102, 172, 172, 0.2);
        border-radius: 50%;
        text-align: center;
        transition: all 0.2s linear;
        &:hover {
          color: #ffffff;
          background-color: rgba(102, 172, 172, 1);
        }
      }
    }
  }
</style>
