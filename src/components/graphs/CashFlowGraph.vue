<script setup lang="ts">
import { ref } from 'vue';

const cardTitle = "Cash Flow";

const options = ref({
    chart: {
        type: 'bar',
        height: 350
    },
    plotOptions: {
        bar: {
            colors: {
                ranges: [{
                    from: -10000,
                    to: 0,
                    color: '#F15B46'
                }, {
                    from: 0,
                    to: -10000,
                    color: '#FEB019'
                }]
            },
            columnWidth: '80%',
        }
    },
    dataLabels: {
        enabled: false,
    },
    xaxis: {
        type: 'datetime',
        categories: [
            '2023-01-01', '2023-02-01', '2023-03-01', '2023-04-01', '2023-05-01', '2023-06-01',
            '2023-07-01', '2023-08-01', '2023-09-01', '2023-10-01', '2023-11-01', '2023-12-01'
        ],
        labels: {
            rotate: -90
        }
    }
});

const series = ref([{
    name: 'Cash Flow',
    data: [456.48, 1274.89, -672.91, -174.84, 843.82, 2014.79, 1285.12, -38.84, 439.03, 790.84, -337.65, 1684.06
    ]
}])


</script>

<template>
    <v-card class="graphCard">
        <v-card-title class="text-center">{{ cardTitle }}</v-card-title>
        <v-card-text>
            <div>
                <apexchart :options="options" :series="series" width="100%"></apexchart>
            </div>
        </v-card-text>
    </v-card>
</template>

<style scoped>
.graphCard {
    height: 400px;
}
</style>