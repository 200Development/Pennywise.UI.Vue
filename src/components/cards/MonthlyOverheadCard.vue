<script setup lang='ts'>
import { ref, computed } from 'vue';
import { Metrics } from '@/models/Metrics';

const monthNames = ["January", "February", "March", "April", "May", "June",
  "July", "August", "September", "October", "November", "December"];

const currentMonth = new Date().getMonth();
const cardTitle = `${monthNames[currentMonth]} Overhead`;
const ExpectedIncome = ref(4300);
const MandatoryExpenses = ref(2450);
const DiscretionarySpending = ref(548);
const Savings = computed(() => {
  return ExpectedIncome.value - TotalMonthlyExpenses.value;
});
const TotalMonthlyExpenses = computed(() => {
  return MandatoryExpenses.value + DiscretionarySpending.value;
});
const expenses = ref<Metrics>({
  items: [
    { label: 'Expected Income', value: ExpectedIncome.value   },   
    { label: 'Mandatory Expenses', value: MandatoryExpenses.value },
    { label: 'Discretionary Spending', value: DiscretionarySpending.value },
    { label: 'Total Expenses', value: TotalMonthlyExpenses.value },
    { label: 'Savings', value: Savings.value }
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
            <v-row v-for="(item, index) in expenses.items" :key="index" no-gutters>
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