<script setup lang='ts'>
import { ref } from 'vue';
import { Metrics } from '@/models/Metrics';

const cardTitle = 'Metrics';
const metrics = ref<Metrics>({
  items: [
    { label: 'Months Covered by Emergency Fund', value: 2.3 },
    { label: 'Trailing Monthly Cash Flow', value: 340 },
    { label: 'Monthly Expense Ratio', value: 0.63 },
    { label: 'Monthly Savings Rate', value: .8 },
    { label: 'Monthly Fixed Expenses Ratio', value: .8 },
    { label: 'Monthly Variable Expenses Ratio', value: .8 }   
  ]
});
</script>

<template>
    <v-card>
        <v-card-title class="text-center">{{ cardTitle }}</v-card-title>
        <v-card-text>
            <v-row v-for="(item, index) in metrics.items" :key="index" no-gutters>
                <v-col cols="6" class="text-left">
                    <div class="left-content">
                        {{ item.label }}
                    </div>
                </v-col>
                <v-col cols="6" class="text-right">
                    <div class="right-content">
                        {{ item.value }}
                    </div>
                </v-col>
                <v-divider></v-divider>
            </v-row>
        </v-card-text>
    </v-card>
</template>

<style scoped></style>