<template>
  <div id="app">
    <img src="./assets/img/back-goku.gif" width="250" style="border-radius: 10px 40px;border: 3px solid #444;">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  width: 100%;
}
</style>
