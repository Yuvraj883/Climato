<template>
<div :style="{backgroundImage:'url(image)'}">
<Navbar/>
  <Display @setImage="setImage" />
  </div>
</template>

<script>
import Display from './components/Display.vue'
import Navbar from './components/Navbar.vue'

export default {
  name: 'App',
  components: {
    Display,
    Navbar
  },
  data(){
    return {
    image:"https://source.unsplash.com/1600x900/? "

    }
  },
  methods:{
setImage(city){
  this.image = this.image+city
}
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
<style scoped>
div{
background-image:url("https://source.unsplash.com/1600x900/? city");

}

</style>
