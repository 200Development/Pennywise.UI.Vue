<script setup lang="ts">
import { computed, ref } from 'vue';
import ExpectedSpendingGraph from '../graphs/ExpectedSpendingGraph.vue';

const monthAbbreviations = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
const currentMonth = new Date().getMonth();
const currentMonthAbbreviation = computed(() => {
    return monthAbbreviations[currentMonth];
});

const totalCumulativeExpenses = ref(0);

function handleCumulativeExpensesUpdate(totalExpenses: number) {
    totalCumulativeExpenses.value = totalExpenses
}
</script>

<template>
    <v-card class="graphCard">
        <v-card-title class="text-center">Expected Spending for {{ currentMonthAbbreviation }} is ${{
            totalCumulativeExpenses?.toFixed() }}</v-card-title>
        <v-card-text>
            <ExpectedSpendingGraph @updateCumulativeExpenses="handleCumulativeExpensesUpdate"></ExpectedSpendingGraph>
        </v-card-text>
    </v-card>
</template>