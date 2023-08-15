<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const chartCanvas = ref(null);
let chartInstance = null;

const pieChartData = {
  labels: ["Red", "Blue", "Yellow", "Green"],
  datasets: [
    {
      data: [30, 20, 30, 20],
      backgroundColor: ["red", "blue", "yellow", "green"],
    },
  ],
};

const newDataValue = ref(null);

onMounted(() => {
  const ctx = chartCanvas.value.getContext("2d");
  chartInstance = new Chart(ctx, {
    type: "pie",
    data: pieChartData,
  });
});

const addDataPoint = () => {
  const newData = Number(newDataValue.value);
  if (!isNaN(newData)) {
    pieChartData.datasets[0].data.push(newData);
    pieChartData.datasets[0].backgroundColor.push(getRandomColor());
    chartInstance.update();
    newDataValue.value = null;
  }
};

const getRandomColor = () => {
  return "#" + Math.floor(Math.random() * 16777215).toString(16);
};

onBeforeUnmount(() => {
  if (chartInstance) {
    chartInstance.destroy();
  }
});

</script>
<template>
  <h1
    class="container mx-auto mt-20 text-4xl text-center text-white bg-gradient-to-r from-yellow-500 via-green-500 via-red-500 to-blue-500 py-5 px-10 font-bold rounded-lg"
  >
    Pie Chart
  </h1>

  <div class="w-[500px] h-[500px] mx-auto py-10">
    <canvas ref="chartCanvas"></canvas>
  </div>

  <div class="flex justify-center items-center gap-3 pb-10">
    <input
      v-model="newDataValue"
      type="number"
      class="p-3 border-none rounded-lg focus:outline-none italic"
      placeholder="Put a Number"
      required
    />

    <button
      type="button"
      @click="addDataPoint"
      class="inline-flex items-center px-5 py-2 text-sm font-medium text-center text-gray-900 bg-white border border-gray-200 rounded-lg hover:bg-gray-100"     
    >
      <span class="text-xl font-bold mr-2"> + </span>
      Add to chart
    </button>
  </div>
</template>

<style scoped></style>
