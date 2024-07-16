<!-- Child component -->
<template id="bar-chart">
    <div class="bar-container">
      <div class="bar" :style="{ width: percentage }">{{ percentage }}</div>
    </div>
</template>
  
<script>  
const BarChart = {
    name: 'BarChart',
    props: {
      percentage: {
        type: String,
        required: true
      }
    }
}
export default BarChart
</script>