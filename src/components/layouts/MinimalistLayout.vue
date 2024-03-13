<script setup lang="ts">
import AppFooter from '@/components/AppFooter.vue';
import MonthlyCashFlowCard from '@/components/cards/MonthlyCashFlowCard.vue';
import MonthlyOverheadCard from '@/components/cards/MonthlyOverheadCard.vue';
import MetricsCard from '@/components/cards/MetricsCard.vue';
import ExpensesTreemapGraph from '@/components/graphs/ExpensesTreemapGraph.vue';
import NetWorthGraph from '@/components/graphs/NetWorthGraph.vue';
import CashFlowGraph from '@/components/graphs/CashFlowGraph.vue';
import ExpectedSpendingGraph from '@/components/graphs/ExpectedSpendingGraph.vue';
import SinkingFundsTable from '@/components/tables/SinkingFundsTable.vue';
import RequiredSavingsGraph from '@/components/graphs/RequiredSavingsGraph.vue';
import Budget from '@/components/Budget.vue';
//import axios from 'axios';
import SinkingFundsCard from '@/components/cards/SinkingFundsCard.vue';

/* async function getUserData () {
    try {
        const response = axios.post('https://localhost:7148/metrics/user')
    } catch (error) {
        
    }
}; */
</script>

<template>
    <v-app>
        <v-main>
            <v-container fluid>
                <v-sheet class="pa-3" elevation="2">
                    <v-row justify="center">
                        <v-col cols="4" class="graphCard">
                            <NetWorthGraph></NetWorthGraph>
                        </v-col>
                        <v-col cols="4" class="graphCard">
                            <CashFlowGraph></CashFlowGraph>
                        </v-col>
                        <v-col cols="4" class="graphCard">
                            <ExpensesTreemapGraph></ExpensesTreemapGraph>
                        </v-col>
                    </v-row>
                </v-sheet>
                <v-sheet class="pa-3" elevation="2">
                    <v-row justify="center">
                        <v-col cols="8">
                            <SinkingFundsCard></SinkingFundsCard>
                        </v-col>
                    </v-row>
                </v-sheet>
                <v-sheet class="pa-3" elevation="2">
                    <v-row>
                        <v-col cols="6">
                            <ExpectedSpendingGraph></ExpectedSpendingGraph>
                        </v-col>
                        <v-col cols="6">
                            <SinkingFundsTable></SinkingFundsTable>
                        </v-col>
                    </v-row>
                </v-sheet>
                <v-sheet class="pa-3" elevation="2">
                    <v-row>
                        <v-col cols="4">
                            <RequiredSavingsGraph></RequiredSavingsGraph>
                        </v-col>
                        <v-col cols="8">
                            <Budget></Budget>
                        </v-col>
                    </v-row>
                </v-sheet>
                <v-sheet class="pa-3" elevation="2">
                    <v-row justify="center">
                        <v-col cols="4">
                            <MonthlyCashFlowCard></MonthlyCashFlowCard>
                        </v-col>
                        <v-col cols="4">
                            <MonthlyOverheadCard></MonthlyOverheadCard>
                        </v-col>
                        <v-col cols="4">
                            <MetricsCard></MetricsCard>
                        </v-col>
                    </v-row>
                </v-sheet>
            </v-container>
        </v-main>
        <AppFooter></AppFooter>
    </v-app>
</template>

<style scoped>
.graphButtonRow {
    justify-content: center;
    height: 50px;
}
</style>