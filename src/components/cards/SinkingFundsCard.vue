<script setup lang="ts">
import { Metrics } from '@/models/Metrics';
import { ref } from 'vue';

const cardTitle = "Sinking Funds";
const sinkingFunds = ref<Metrics>({
    items: [
        {label: "Insurance", value: 400},
        {label: "Groceries", value: 331},
        {label: "Rent", value: 995},
        {label: "Vacation", value: 1029},
        {label: "Auto Repair", value: 298},
        {label: "Loan Repayment", value: 148},
        {label: "Subscriptions", value: 83},
        {label: "Shopping", value: 372},
        {label: "Bills and Utilities", value: 147},
    ]
});

const formatCurrency = (amount: number) => {
  return new Intl.NumberFormat('en-US', { 
    style: 'currency', 
    currency: 'USD' 
  }).format(amount);
};
</script>

<template>
 <v-card>
        <v-card-title class="text-center">{{ cardTitle }}</v-card-title>
        <v-card-text>
            <v-row v-for="(item, index) in sinkingFunds.items" :key="index" no-gutters>
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
        </v-card-text>
    </v-card>
</template>