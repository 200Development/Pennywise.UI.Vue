<script setup lang='ts'>
import { ref } from 'vue';
import { Metrics } from '@/models/Metrics';
//import axios from 'axios';

const cardTitle = 'Savings';
const savings = ref<Metrics>({
  items: [
    { label: 'Total Cash', value: 1000 },
    { label: 'Cash Until Next Payday', value: 650 },
    { label: 'Remaining Cash Balance', value: 310 }
  ]
});

/* async function getSavingsMetrics() {
  try {
    const data = { userId: 1 }
    const response = await axios.post('https://localhost:7148/metrics/savings', data);
    
    
  } catch (err) {
    console.error('Failed to get accounts: ', err);
  }
}; */

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
            <v-row v-for="(item, index) in savings.items" :key="index" no-gutters>
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