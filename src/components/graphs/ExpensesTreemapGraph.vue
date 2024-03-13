<script setup lang="ts">
import { ref } from 'vue';

const options = ref({
  chart: {
    height: 200,
    type: "treemap",
  },
  plotOptions: {
    treemap: {
      colorScale: {
        ranges: [
          {
            from: 0,
            to: 200,
            color: '#CD363A'
          },
          {
            from: 201,
            to: 1000,
            color: '#52B12C'
          }
        ]
      }
    }
  },
});

const series = ref([
  {
    data: [
      {
        x: "Rent/Mortgage",
        y: 1950,
      },
      {
        x: "Other",
        y: 149,
      },
      {
        x: "Bills & Utilities",
        y: 216,
      },
      {
        x: "Shopping",
        y: 351,
      },
      {
        x: "Uncategorized",
        y: 420,
      },
      {
        x: "Financial",
        y: 500,
      },
      {
        x: "Education",
        y: 525,
      },
      {
        x: "Auto & Transport",
        y: 641,
      },
      {
        x: "Entertainment",
        y: 677,
      },
      {
        x: "Food & Dining",
        y: 839,
      }
    ],
  },
]);
</script>

<template>
  <div>
    <apexchart :options="options" type="treemap" width="100%" :series="series"></apexchart>
  </div>
</template>