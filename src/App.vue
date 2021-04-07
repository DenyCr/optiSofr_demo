<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png">
    <PageGrid :cols="cols" :response="data" />
  </div>
</template>

<script>
import PageGrid from './components/pageGrid'
import cols from './data/cols/gridCols'
import data from './data/data/testdata'

export default {
  name: 'App',
  components: {
    PageGrid
  },
  data () {
    return {
      cols,
      data,
    }
  }
}
</script>

<style>
#app {
  position: relative;

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  display: flex;
  text-align: center;
  justify-content: center;
  align-items: center;

  color: #2c3e50;
  margin: 60px auto;
  width: 100vw;
  overflow-x: hidden;
}
</style>
