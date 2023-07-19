<template>
  <div id="app">
    <QrLector />
  </div>
</template>

<script>
import QrLector from './components/QrLector.vue';
export default {
  name: 'app',
  components: {
    QrLector
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
