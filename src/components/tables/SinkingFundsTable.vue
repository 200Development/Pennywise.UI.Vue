<script setup lang='ts'>
import { ref } from 'vue';

const items = ref([
    { 'Sinking_Fund': 'Groceries', 'Required_Savings': 55.25, 'Current_Savings': 50.00 },
    { 'Sinking_Fund': 'Rent', 'Required_Savings': 600.00, 'Current_Savings': 550.00 },
    { 'Sinking_Fund': 'Gas', 'Required_Savings': 100.00, 'Current_Savings': 75.00 },
].map(item => ({
    ...item,
    'Difference': (item['Required_Savings'] - item['Current_Savings']).toFixed(2),
})));


const headers = ref([
    { title: 'Sinking Fund', value: 'Sinking_Fund', key: 'Sinking_Fund', sortable: true },
    { title: 'Required Savings', value: 'Required_Savings', key: 'Required_Savings', sortable: true },
    { title: 'Current Savings', value: 'Current_Savings', key: 'Current_Savings', sortable: true },
    { title: '+/-', value: 'Difference', key: 'Difference' },
]);

function formatCurrency(value) {
    return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(value);
}
</script>


<template>
    <v-card>
        <v-card-title></v-card-title>
        <v-card-text>
            <div class="sinkingFundsTable">
                <v-data-table :headers="headers" :items="items" height="350px">
                    <template v-slot:[`item.Sinking_Fund`]="{ item }">
                        {{ item['Sinking_Fund'] }}
                    </template>
                    <template v-slot:[`item.Required_Savings`]="{ item }">
                        {{ formatCurrency(item['Required_Savings']) }}
                    </template>
                    <template v-slot:[`item.Current_Savings`]="{ item }">
                        {{ formatCurrency(item['Current_Savings']) }}
                    </template>
                    <template v-slot:[`item.Difference`]="{ item }">
                        {{ formatCurrency(item['Difference']) }}
                    </template>
                </v-data-table>
            </div>
        </v-card-text>
    </v-card>
</template>
  
<style>
.sinkingFundsTable {
    min-height: 400px;
}
</style>
  