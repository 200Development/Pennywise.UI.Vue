<script setup lang="ts">
import { computed, ref, watch, onMounted } from 'vue';

const emit = defineEmits(['updateCumulativeExpenses']);

onMounted(() => {
  // Emit the total cumulative expenses when the component mounts
  // This ensures that the parent component receives the initial value.
  emit('updateCumulativeExpenses', totalCumulativeExpenses.value);
});

const expensesData = [
  { day: 1, expense: 100, description: "Groceries" },
  { day: 5, expense: 50, description: "Transportation" },
  { day: 10, expense: 150, description: "Utilities" },
  { day: 15, expense: 200, description: "Rent" },
  { day: 20, expense: 75, description: "Entertainment" },
  { day: 25, expense: 100, description: "Miscellaneous" }
];

const totalCumulativeExpenses = computed(() => {
  return cumulativeExpenses.value.at(-1); // Get the last element which is the total of cumulative expenses
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
  <div>
    <apexchart :options="options" :series="series" width="100%" height="350"></apexchart>
  </div>
</template>