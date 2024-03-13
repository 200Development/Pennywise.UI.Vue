<script setup lang="ts">
import AppFooter from '@/components/AppFooter.vue';
import MonthlyCashFlowCard from '@/components/cards/MonthlyCashFlowCard.vue';
import MonthlyOverheadCard from '@/components/cards/MonthlyOverheadCard.vue';
import MetricsCard from '@/components/cards/MetricsCard.vue';
import SinkingFundsTable from '@/components/tables/SinkingFundsTable.vue';
import SinkingFundsCard from '@/components/cards/SinkingFundsCard.vue';
import CashFlowCard from '../cards/CashFlowCard.vue';
import ExpensesTreemapCard from '../cards/ExpensesTreemapCard.vue';
import NetWorthCard from '../cards/NetWorthCard.vue';
import ExpectedSpendingCard from '../cards/ExpectedSpendingCard.vue';
import RequiredSavingsCard from '../cards/RequiredSavingsCard.vue';
import BudgetCard from '../cards/BudgetCard.vue';
//import axios from 'axios';

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
                            <NetWorthCard></NetWorthCard>
                        </v-col>
                        <v-col cols="4" class="graphCard">
                            <CashFlowCard></CashFlowCard>
                        </v-col>
                        <v-col cols="4" class="graphCard">
                            <ExpensesTreemapCard></ExpensesTreemapCard>
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
                            <ExpectedSpendingCard></ExpectedSpendingCard>
                        </v-col>
                        <v-col cols="6">
                            <SinkingFundsTable></SinkingFundsTable>
                        </v-col>
                    </v-row>
                </v-sheet>
                <v-sheet class="pa-3" elevation="2">
                    <v-row>
                        <v-col cols="4">
                            <RequiredSavingsCard></RequiredSavingsCard>
                        </v-col>
                        <v-col cols="8">
                            <BudgetCard></BudgetCard>
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