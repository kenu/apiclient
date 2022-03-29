<template>
  <div id="app">
    <ApiClient msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import ApiClient from './components/ApiClient.vue'

export default {
  name: 'App',
  components: {
    ApiClient
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
