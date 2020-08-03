<template>
  <div id="app">
    <h1>Les bons artisans</h1>
    <Home smartphone="smartphones"/>
  </div>
</template>

<script>

 import Home from '../src/components/Home';
export default {
  name: 'App',
  components: {
    Home,
  },
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
