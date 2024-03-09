<script setup lang="ts">
import AppFooter from '@/components/AppFooter.vue';
import SavingsCard from '@/components/cards/SavingsCard.vue';
import OverheadCard from '@/components/cards/OverheadCard.vue';
import MetricsCard from '@/components/cards/MetricsCard.vue';
import ExpensesTreemapGraph from '@/components/graphs/ExpensesTreemapGraph.vue';
import NetWorthGraph from '@/components/graphs/NetWorthGraph.vue';
import CashFlowGraph from '@/components/graphs/CashFlowGraph.vue';
import ExpectedSpendingGraph from '../graphs/ExpectedSpendingGraph.vue';
import SinkingFundsTable from '../tables/SinkingFundsTable.vue';
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
                    <v-row class="graphButtonRow">
                        <v-btn elevation="2">Button</v-btn>
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
                    <v-row justify="center">
                        <v-col cols="4">
                            <SavingsCard></SavingsCard>
                        </v-col>
                        <v-col cols="4">
                            <OverheadCard></OverheadCard>
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