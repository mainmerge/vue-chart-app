<template>
  <div style="position: relative; height: 50vh; width: 90vw; max-width: 800px; margin: auto;">
    <Bar v-if="loaded" :data="chartData" :options="chartOptions" />
    <p v-else>Загрузка графика...</p>
  </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import { Bar } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale);

const mockData = [
  { name: "Январь", value: 150 },
  { name: "Февраль", value: 200 },
  { name: "Март", value: 180 },
  { name: "Апрель", value: 220 },
  { name: "Май", value: 300 },
  { name: "Июнь", value: 250 },
];

const loaded = ref(false);
const chartData = ref({});
const chartOptions = ref({
  responsive: true,
  plugins: {
    title: {
      display: true,
      text: 'Гистограмма данных по месяцам',
    },
  },
});

onMounted(() => {
  setTimeout(() => {
    chartData.value = {
      labels: mockData.map(item => item.name),
      datasets: [
        {
          label: 'Значения по месяцам',
          data: mockData.map(item => item.value),
          backgroundColor: '#41B883',
        },
      ],
    };
    loaded.value = true;
  }, 1000);
});
</script>