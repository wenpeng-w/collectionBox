<template>
  <div>
    <v-header></v-header>
    <router-view :hotSpots="hotSpots"></router-view>
    <v-footer></v-footer>
    <go-top></go-top>
  </div>
</template>

<script>
import Header from './components/header'
import Footer from './components/footer'
import GoTop from './components/goTop'

const ERR_OK = 0

export default {
  data () {
    return {
      hotSpots: {
        type: Object
      }
    }
  },
  created () {
    this.$http.get('/api/collection').then((response) => {
      response = response.body
      if (response.errno === ERR_OK) {
        this.hotSpots = Object.assign({}, this.hotSpots, response.data)
      }
    })
  },
  components: {
    'v-header': Header,
    'v-footer': Footer,
    GoTop
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
