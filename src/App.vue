<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div>
      
        <div><router-link to="/HelloWorld">GO to HelloWorld</router-link></div>
        <div><router-link to="/HelloPaul">GO to Calculate</router-link></div>
        <div><router-link to="/HelloVue">GO to Vue</router-link></div>
        <div><router-link to="/HelloSass">GO to Sass</router-link></div>
      
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style >
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
