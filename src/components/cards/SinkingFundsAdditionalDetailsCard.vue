<script setup lang="ts">
import { SinkingFundsModel } from '@/models/SinkingFundsModel';
import { ref, computed } from 'vue';

const props = defineProps<{
    fund?: SinkingFundsModel
}>();

function FormatMonth(monthDiff: number){
    let currentDate = new Date();
    const options: Intl.DateTimeFormatOptions = { month: 'short', year: '2-digit' };
    const currentMonth = currentDate.getMonth();
    currentDate.setMonth(currentMonth + monthDiff);
    
    // Handle year change if current month is December
    if(currentMonth === 11) {
        currentDate.setFullYear(currentDate.getFullYear() + 1);
    }; 

    return new Intl.DateTimeFormat('en-us',options).format(currentDate);
}   

const series = ref([{
    name: 'Withdrawls',
    type: 'column',
    data: [100, 25, 0, 0, 50, 0, 80, 45, 25]
}, {
    name: 'Contributions',
    type: 'column',
    data: [80, 80, 80, 80, 80, 80, 80, 80, 80]
}, {
    name: 'Balance',
    type: 'line',
    data: [20, 75, 155, 235, 265, 345, 389, 433, 477]
}]);

const chartOptions = computed(() => ({
    chart: {
        height: 350,
        type: 'line',
        stacked: false
    },
    dataLabels: {
        enabled: false
    },
    stroke: {
        width: [1, 1, 3, 3],
        dashArray: [0, 0, 0]
    },
    markers: {
        size: [4, 4]
    },
    title: {
        text: props.fund ? `${props.fund.label} Sinking Fund` : '',
        align: 'left',
        offsetX: 110
    },
    xaxis: {
        categories: [FormatMonth(-5), FormatMonth(-4), FormatMonth(-3), FormatMonth(-2), FormatMonth(-1), FormatMonth(0), FormatMonth(1), FormatMonth(2), FormatMonth(3)],
    },
    yaxis: [
        {
            axisTicks: {
                show: true,
            },
            axisBorder: {
                show: true,
                color: '#008FFB'
            },
            labels: {
                style: {
                    colors: '#008FFB',
                }
            },
            title: {
                text: "Withdrawls",
                style: {
                    color: '#008FFB',
                }
            },
            tooltip: {
                enabled: true
            }
        },
        {
            seriesName: 'Withdrawls',
            opposite: true,
            axisTicks: {
                show: true,
            },
            axisBorder: {
                show: true,
                color: '#00E396'
            },
            labels: {
                style: {
                    colors: '#00E396',
                }
            },
            title: {
                text: "Contributions",
                style: {
                    color: '#00E396',
                }
            },
        },
        {
            seriesName: 'Contributions',
            opposite: true,
            axisTicks: {
                show: true,
            },
            axisBorder: {
                show: true,
                color: '#FEB019'
            },
            labels: {
                style: {
                    colors: '#FEB019',
                },
            },
            title: {
                text: "Balance",
                style: {
                    color: '#FEB019',
                }
            }
        },
       
    ],
    tooltip: {
        fixed: {
            enabled: true,
            position: 'topLeft', // topRight, topLeft, bottomRight, bottomLeft
            offsetY: 30,
            offsetX: 60
        },
    },
    legend: {
        horizontalAlign: 'left',
        offsetX: 40
    }
})
);
</script>

<template>
    <v-card v-if="fund">
        <div id="chart">
            <apexchart type="line" height="350" :options="chartOptions" :series="series"></apexchart>
        </div>
    </v-card>
</template>