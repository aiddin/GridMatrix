<template>

  <GridChart :row="row"
  :column="column"
  :isVisible="isVisible"
  :highlight="highlight"
  :cellColor="cellColor"
  :endPoint="endPoint"
 
  />

</template>

<script>
import GridChart from './components/GridChart.vue'

export default {
  name: 'App',
  components: {
    GridChart
    
  },
  data(){
    return {
      row:5,
      column:5,
      isVisible: true,
      highlight : 'blue',
      cellColor: '#808080',
      endPoint: '#FFD700'
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
