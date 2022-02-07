<template>
  
  <router-view/>

  <div class="text-center mt-5 mb-3">
  <img src="@/assets/logo.png" class="rounded" style="max-width:30px;"  alt="..."> <a href="https://vuejs.org/" target="_blank">Vue.js</a>
</div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

a{
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;
}

a:hover{
  color:#42b983
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
