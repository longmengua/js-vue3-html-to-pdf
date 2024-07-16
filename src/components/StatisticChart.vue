<template>
  <div>
    <BarChart percentage="70%" />
    <BarChart percentage="50%" />
    <BarChart percentage="85%" />
  </div>
</template>

<script>
import BarChart from './BarChart.vue'
export default {
  name: 'HorizontalBarChart',
  components: {
    BarChart
  }
}
</script>

<style>
.bar-container {
  width: 300px;
  height: 30px;
  background-color: #f0f0f0;
  border-radius: 5px;
  margin: 20px;
  overflow: hidden;
}

.bar {
  height: 100%;
  background-color: #4CAF50;
  text-align: right;
  line-height: 30px;
  color: white;
  transition: width 0.6s ease;
}
</style>
