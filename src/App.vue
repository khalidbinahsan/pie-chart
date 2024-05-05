<script setup>
import { ref, onMounted } from 'vue'
import Chart from 'chart.js/auto';
const itemLabel = ref()
const itemNumber = ref(16)
let chart = null
const myLabels = ['Egg', 'Banana', 'Lychee']
const myData = [300, 50, 100]
const data = {
  labels: myLabels,
  datasets: [{
    label: 'Total sell',
    data: myData,
    backgroundColor: [
      'rgb(255, 99, 132)',
      'rgb(54, 162, 235)',
      'rgb(255, 205, 86)'
    ],
    hoverOffset: 4
  }]
};
const config = {
  type: 'pie',
  data: data,
};
onMounted(() => {
  const ctx = document.getElementById('chart')
  chart = new Chart(ctx, config);
})
function updateChart() {
  myLabels.push(itemLabel.value)
  myData.push(itemNumber.value)
  chart.data.labels = myLabels
  chart.data.datasets[0].data = myData
  chart.update()
}

</script>

<template>
  <div class="mx-auto w-[400px] h-[400px] bg-gray-400 mt-10 p-5">
    <canvas id="chart">
    </canvas>
  </div>
  <div class="mt-5 flex flex-col gap-4 mx-auto max-w-[400px] p-5 border border-gray-400">
    <input type="text" v-model="itemLabel" class="border p-2" placeholder="Chart Label">
    <input type="number" v-model="itemNumber" class="border p-2">
    <button @click="updateChart()" class="ml-2 bg-blue-500 text-white font-bold py-2 px-8 rounded">Add</button>
  </div>
</template>

<style scoped>

</style>
