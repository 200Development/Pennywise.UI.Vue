<script setup lang="ts">
import { computed, ref } from 'vue';


const expensesData = [
  { day: 1, expense: 100, description: "Groceries" },
  { day: 5, expense: 50, description: "Transportation" },
  { day: 10, expense: 150, description: "Utilities" },
  { day: 15, expense: 200, description: "Rent" },
  { day: 20, expense: 75, description: "Entertainment" },
  { day: 25, expense: 100, description: "Miscellaneous" }
];

const monthAbbreviations = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
const currentMonth = new Date().getMonth(); 
const currentMonthAbbreviation = computed(() => {
  return monthAbbreviations[currentMonth];
});


// Calculate the cumulative expenses
const cumulativeExpenses = computed(() => {
  return expensesData.reduce((acc: number[], curr, index) => {
    if (index === 0) {
      acc.push(curr.expense);
    } else {
      acc.push(acc[index - 1] + curr.expense);
    }
    return acc;
  }, []);
});

const totalCumulativeExpenses = computed(() => {
  return cumulativeExpenses.value.at(-1); // Get the last element which is the total of cumulative expenses
});

// Update series data with cumulative expenses
const series = computed(() => [
  {
    name: "Expenses",
    data: expensesData.map((item, index) => ({
      x: item.day,
      y: cumulativeExpenses.value[index],
    })),
  },
]);

const options = ref({
  chart: {
    height: 150,
    type: 'line',
    toolbar: {
      show: false,
    },
  },
  xaxis: {
    type: 'numeric',
    categories: expensesData.map(item => item.day),
    title: {
      text: 'Day of the Month',
    },
  },
  yaxis: {
    title: {
      text: 'Expenses ($)',
    },
  },
  annotations: {
    points: expensesData.map(item => ({
      x: item.day,
      y: item.expense,
      marker: {
        size: 8,
      },
      label: {
        borderColor: '#FF4560',
        offsetY: 0,
        style: {
          color: '#fff',
          background: '#FF4560',
        },
        text: item.description,
      },
    })),
  },
});
</script>

<template>
  <v-card class="graphCard">
    <v-card-title class="text-center">Expected Spending for {{ currentMonthAbbreviation }} is ${{ totalCumulativeExpenses?.toFixed() }}</v-card-title>
    <v-card-text>
      <div>
        <apexchart :options="options" :series="series" width="100%" height="350"></apexchart>
      </div>
    </v-card-text>
  </v-card>
</template>