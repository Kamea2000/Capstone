<template>
  <div class="chart-container">
    <Line :data="chartData" :options="chartOptions" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { Line } from 'vue-chartjs';
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement,
} from 'chart.js';

// Register the required components for Chart.js
ChartJS.register(Title, Tooltip, Legend, LineElement, CategoryScale, LinearScale, PointElement);

// Chart data and options
const chartData = ref({
  labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
  datasets: [
    {
      label: 'Sales Over Time',
      backgroundColor: 'rgba(75, 192, 192, 0.2)',
      borderColor: 'rgba(75, 192, 192, 1)',
      borderWidth: 2,
      tension: 0.4,
      pointBackgroundColor: 'rgba(75, 192, 192, 1)',
      data: [40, 39, 10, 40, 39, 80, 40], // Sample data
    },
  ],
});

const chartOptions = ref({
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: {
      display: true,
    },
    tooltip: {
      intersect: false,
    },
  },
  scales: {
    y: {
      beginAtZero: true,
      ticks: {
        color: '#6b7280', // Tailwind gray
      },
      grid: {
        color: '#d1d5db', // Tailwind light gray
      },
    },
    x: {
      ticks: {
        color: '#6b7280', // Tailwind gray
      },
      grid: {
        color: '#d1d5db', // Tailwind light gray
      },
    },
  },
});
</script>

<style scoped>
.chart-container {
  position: relative;
  height: 400px; /* Adjust height based on your layout */
  padding: 20px; /* Optional padding */
  background-color: aliceblue;
}
</style>
