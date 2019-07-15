<template>
  <div id="app">
    <calcvuejs/>
  </div>
</template>

<script>
import calcvuejs from './components/calcvuejs'

export default {
  name: 'App',
  components: {
    calcvuejs
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
