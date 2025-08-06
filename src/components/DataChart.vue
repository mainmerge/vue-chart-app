<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import { Bar } from 'vue-chartjs';
import {Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale} from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale);

const chartData = ref({});
const loaded = ref(false);
const chartOptions = ref({
  responsive: true,
  plugins: {
    title: {
      display: true,
      text: 'Гистограмма данных'
    }
  }
});

onMounted(async () => {
  try {
    const response = await axios.get('https://service-apm.ru/test_json.php');
    const apiData = response.data.data;

    chartData.value = {
      labels: Object.keys(apiData),
      datasets: [
        {
          label: 'Значения',
          backgroundColor: '#42A5F5',
          data: Object.values(apiData),
        },
      ],
    };
    loaded.value = true;
  } catch (error) {
    console.error(error);
  }
});
</script>

<template>
  <div style="width: 600px; height: 400px; margin: auto;">
    <Bar v-if="loaded" :data="chartData" :options="chartOptions"/>
    <p v-else>Загрузка графика...</p>
  </div>
</template>