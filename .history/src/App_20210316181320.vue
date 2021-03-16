<template>
  <div id="app">
    <Nav></Nav>
    <router-view />
  </div>
</template>

<script>
import Nav from '@/components/Nav'
export default {
  name: 'App',
  components: {
    Nav
  }
}
</script>

<style>
html,
body {
    margin: 0;
    padding: 0;
    font-size: 20px;
    font-family: Raleway, Arial, Helvetica, sans-serif;
}

#app {
  font-family: Raleway, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 100vw;
  height: 100vw;
  background-color: #6baaa1;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}
</style>
