<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
  #app {
    margin: 0;
    border: 0;
    padding: 0;
    height: 100%;
    width: 100%;

    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    padding-top: 60px;
    color: #fff;
    background-color: #000;
    height: 100%;
  }
</style>
