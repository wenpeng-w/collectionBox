<template>
  <div>
    <v-header></v-header>
    <router-view></router-view>
  </div>
</template>

<script>
import Header from './components/header'
export default {
  data () {
    return {}
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
