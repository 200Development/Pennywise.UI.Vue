<script setup lang="ts">
import { ref } from 'vue';

const options = ref({
    chart: {
        height: 200,
        type: 'line',
        zoom: {
            enabled: false
        }
    },
    dataLabels: {
        enabled: false
    },
    stroke: {
        curve: 'straight'
    },
    title: {
        text: 'Monthly',
        align: 'left'
    },
    grid: {
        row: {
            colors: ['#f3f3f3', 'transparent'], // takes an array which will be repeated on columns
            opacity: 0.5
        },
    },
    xaxis: {
        categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep'],
    },
    yaxis: {
    labels: {
      formatter: function (val: number) {
        return '$' + val.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 });
      }
    }
  },
    tooltip: {
        y: {
            formatter: function (val: number) {
                return '$' + val.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 });
            }
        }
    },
});

const series = ref([{
    name: "Net Worth",
    data: [98389, 99467, 99149, 101302, 102665, 103280, 105810, 103929, 104398]
}]);
</script>

<template>
    
            <div>
                <apexchart width="100%" :options="options" :series="series" type="line"></apexchart>
            </div>
       
</template>
