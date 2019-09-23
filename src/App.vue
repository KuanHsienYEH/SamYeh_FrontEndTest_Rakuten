<template>
  <div id="app">
    <img src="./assets/logo.png">
    <page/>
  </div>
</template>

<script>
import page from './components/page/page'

export default {
  name: 'App',
  components: {
    page
  }
}
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
