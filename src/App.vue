<template>
  <div>
    <v-header></v-header>
    <router-view :hotSpots="hotSpots"></router-view>
  </div>
</template>

<script>
import Header from './components/header'

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
        console.log(response)
        this.hotSpots = Object.assign({}, this.hotSpots, response.data)
      }
    })
  },
  components: {
    'v-header': Header
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
