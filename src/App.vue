<template>
  <div id="app">
    <router-view/>
    <footerComp/>
  </div>
</template>

<script>
import footerComp from '@/components/footerComp.vue'
  export default {
    components: {
      footerComp,
    },
  }
</script>
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
    background-size: cover;
   width:100%;
  min-height: 100vh;
   padding:0;
   margin: 0;
}
body{
  min-height: 100vh;
      background-size: cover;
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
a{
  text-decoration:none;

}
</style>
