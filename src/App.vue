<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
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
body {
  background: url(./assets/bg2.jpg) no-repeat;
  /* background-color: #fff7e2; */
   background-size: 100% 100%;
    /* background: linear-gradient(#c9eded,#e6f1f1,#bfdfdb); */
   /* background-size: cover; */
      height: 800px;
      max-width: 500px;
      min-width: 365px;
      margin: 0 auto;
}
</style>
