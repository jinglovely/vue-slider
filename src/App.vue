<template>
  <div id="app" >
    
    <slider id='slider'></slider>
  </div>
</template>

<script>
import slider from './components/slider'

export default {
  name: 'App',
  components: {
    slider
  },
  methods:{
   
  }
}
</script>

<style>
*{
  box-sizing: border-box;
  margin:0;
  padding:0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
 
  padding: 0 400px;
  
  height: 800px;

  
 
}


#slider {

    margin-top:100px;

  }

</style>
