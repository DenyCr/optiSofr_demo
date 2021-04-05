<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <PageGrid :cols="cols" :response="data" />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import PageGrid from './components/pageGrid'
import cols from './data/cols/gridCols'
import data from './data/data/testdata'

export default {
  name: 'App',
  components: {
    HelloWorld,
    PageGrid
  },
  data () {
    return {
      cols,
      data
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
