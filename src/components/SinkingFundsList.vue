<script setup lang="ts">
import { SinkingFundsModel } from '@/models/SinkingFundsModel';
import { ref } from 'vue';

const emit = defineEmits(['fund-selected'])
const selectedFund = ref('')
const sinkingFunds = ref<Array<SinkingFundsModel>>(
    [
        {id: "1", label: "Insurance", value: 400},
        {id: "2", label: "Groceries", value: 331},
        {id: "3", label: "Rent", value: 995},
        {id: "4", label: "Vacation", value: 1029},
        {id: "5", label: "Auto Repair", value: 298},
        {id: "6", label: "Loan Repayment", value: 148},
        {id: "7", label: "Subscriptions", value: 83},
        {id: "8", label: "Shopping", value: 372},
        {id: "9", label: "Bills and Utilities", value: 147},
    ]
);

const formatCurrency = (amount: number) => {
    return new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD'
    }).format(amount);
};

function selectFund(fund: any) {
    selectedFund.value = fund;
    console.log(`selected fund: ${JSON.stringify(fund)}`)
    emit('fund-selected', fund);
};
</script>

<template>
    <v-row v-for="(item, index) in sinkingFunds" :key="index" @click="selectFund(item)" no-gutters>
        <v-col cols="6" class="text-left">
            <div class="left-content">
                {{ item.label }}
            </div>
        </v-col>
        <v-col cols="6" class="text-right">
            <div class="right-content">
                {{ formatCurrency(item.value) }}
            </div>
        </v-col>
        <v-divider></v-divider>
    </v-row>
</template>

<style scoped>
.v-row:hover {
    cursor: pointer;
    background-color: #f9f9f9; /* Light grey background on hover */
}
</style>