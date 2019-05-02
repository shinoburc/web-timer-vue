<template>
  <div id="app">
    <WebTimer/>
  </div>
</template>

<script>
import WebTimer from './components/WebTimer'

export default {
  name: 'app',
  components: {
    WebTimer
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
