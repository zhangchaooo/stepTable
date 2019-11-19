<template>
  <div id="app">
    <router-link to='/step'>Steptble</router-link> |
    <router-link to='/step02'>Steptble02</router-link> |
    <router-link to='/'>Home</router-link> |
    <router-link to='/about'>About</router-link>
    <router-view></router-view>
  </div>
</template>

<script>

export default {
  name: 'app'
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin: 60px 60px;
}
li {
  list-style: none;
}
</style>
