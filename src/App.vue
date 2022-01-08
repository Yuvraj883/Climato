<template>
<Navbar/>
  <Display />
  
</template>

<script>
import Display from './components/Display.vue'
import Navbar from './components/Navbar.vue'

export default {
  name: 'App',
  components: {
    Display,
    Navbar
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
