<script setup lang='ts'>
import { ref, computed } from 'vue';
import { Metrics } from '@/models/Metrics';

const cardTitle = 'Overhead';
const FixedMonthlyExpenses = ref(2450);
const DiscretionaryMonthlyExpenses = ref(548);
const RemainingMonthlyExpenses = ref(874.49);
const TotalMonthlyExpenses = computed(() => {
  return FixedMonthlyExpenses.value + DiscretionaryMonthlyExpenses.value;
});
const expenses = ref<Metrics>({
  items: [
    { label: 'Due Before Next Payday', value: 430 },
    { label: 'Total Monthly Expenses', value: TotalMonthlyExpenses.value },
    { label: 'Fixed Monthly Expenses', value: FixedMonthlyExpenses.value },
    { label: 'Discretionary Monthly Spending', value: DiscretionaryMonthlyExpenses.value },
    { label: 'Remaining Monthly Expenses', value: RemainingMonthlyExpenses.value }
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