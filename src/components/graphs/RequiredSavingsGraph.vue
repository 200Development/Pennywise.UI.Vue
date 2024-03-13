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

const requiredSavings = ref([100, 112, 125, 100, 50, 75, 80, 90, 125]);
const currentSavings = ref([80, 110, 125, 100, 80, 100, 80, 80, 80]);

// Computed property to calculate the difference dynamically
const difference = computed(() => {
  return requiredSavings.value.map((req, index) => req - currentSavings.value[index]);
});

const series = computed(() => [
  {
    name: 'Required Savings',
    type: 'column',
    data: requiredSavings.value
  },
  {
    name: 'Actual Savings',
    type: 'column',
    data: currentSavings.value
  },
  {
    name: 'Difference',
    type: 'line',
    data: difference.value // Use the computed difference
  }
]);

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
        text: props.fund ? `${props.fund.label} Required Savings` : '',
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
                text: "Required Savings",
                style: {
                    color: '#008FFB',
                }
            },
            tooltip: {
                enabled: true
            }
        },
        {
            seriesName: 'Required Savings',
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
                text: "Current Savings",
                style: {
                    color: '#00E396',
                }
            },
        },
        {
            seriesName: 'Current Savings',
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
                text: "Difference",
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
        <div>
            <apexchart type="line" height="400px" width="100%" :options="chartOptions" :series="series"></apexchart>
        </div>
</template>