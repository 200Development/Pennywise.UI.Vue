<script setup lang='ts'>
import { ref } from 'vue';
import { Metrics } from '@/models/Metrics';
//import axios from 'axios';

const cardTitle = 'Cash Flow Snapshot';
const savings = ref<Metrics>({
  items: [
    { label: 'Last Paycheck', value: 3000 },
    { label: 'Current Savings', value: 4300 },   
    { label: 'Mandatory Expenses', value: 2200 },
    { label: 'Recommended Savings', value: 2000 },
    { label: 'Disposable Income Until Next Paycheck', value: 100 },
  ]
});
const nextPayday = ref(new Date(2024,3,15));
const formattedNextPayday = formatDate(nextPayday.value);


function formatDate(date: Date) {
  const formattedDate = date.toLocaleDateString('en-US');
  const dayOfWeek = date.toLocaleDateString('en-US', { weekday: 'short' });
  return `${dayOfWeek} ${formattedDate}`;
};


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
      <v-row justify="center" class="my-4 py-2" style="background-color: rgba(0,0,0,0.05);">
        <v-col cols="12" class="text-center">
          Next Paycheck is due <strong>{{ formattedNextPayday }}</strong>
        </v-col>
      </v-row>
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

<style scoped>
.left-content, .right-content {
  padding: 8px 0; /* Adjust padding as needed */
}
</style>
