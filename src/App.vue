<template>
  <Main/>
  <Footer/>
</template>

<script>
import Main from './components/Main.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Main,
    Footer
  }
}
</script>

<style>
* {
margin: 0;
padding: 0;
}
html, body{
  font-family: sans-serif;
  width: 100%;
  height: 100%;
}
a{
  text-decoration: none;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100%;
  height: 100%;
}

</style>
