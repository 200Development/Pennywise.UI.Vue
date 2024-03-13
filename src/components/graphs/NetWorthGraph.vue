<script setup lang="ts">
import { ref } from 'vue';

const cardTitle = "Net Worth";

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
    <v-card class="graphCard">
        <v-card-title class="text-center">{{ cardTitle }}</v-card-title>
        <v-card-text>
            <div>
                <apexchart width="100%" :options="options" :series="series" type="line"></apexchart>
            </div>
        </v-card-text>
    </v-card>
</template>

<style scoped>
.graphCard {
    height: 400px;
}
</style>