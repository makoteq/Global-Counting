<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
@import './assets/colors.scss';
@import url('https://fonts.googleapis.com/css?family=Source+Code+Pro:400,900&display=swap&subset=latin-ext');
#app {
  font-family: 'Source Code Pro', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
    background-color: $main;
   width:100vw;
   height: 100vh;
   padding:0;
   margin: 0;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
