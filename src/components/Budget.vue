<template>
    <v-container>
      <!-- Budget Overview -->
      <v-row class="mb-2">
        <v-col cols="12" md="4" class="py-1">
          <v-card class="pa-2" outlined>
            Total Income: {{ formatCurrency(totalIncome) }}
          </v-card>
        </v-col>
        <v-col cols="12" md="4" class="py-1">
          <v-card class="pa-2" outlined>
            Total Expenses: {{ formatCurrency(totalExpenses) }}
          </v-card>
        </v-col>
        <v-col cols="12" md="4" class="py-1">
          <v-card :color="net >= 0 ? 'green lighten-4' : 'red lighten-4'" class="pa-2" outlined>
            <div v-if="net >= 0">
              Savings: {{ formatCurrency(net) }}
            </div>
            <div v-else>
              Shortfall: {{ formatCurrency(Math.abs(net)) }}
            </div>
          </v-card>
        </v-col>
      </v-row>
      <!-- Sinking Funds -->
      <v-row>
        <v-col cols="12">
          <v-card>
            <v-card-title class="text-h6">Sinking Funds</v-card-title>
            <v-list>
              <v-list-item v-for="(fund, index) in funds" :key="index" class="py-1">
                <v-list-item-content>
                  <v-list-item-title class="subtitle-1">{{ fund.name }}</v-list-item-title>
                  <v-list-item-subtitle>
                    Target: {{ formatCurrency(fund.targetAmount) }},
                    Current: {{ formatCurrency(fund.currentAmount) }}
                  </v-list-item-subtitle>
                  <v-slider
                    v-model="fund.currentAmount"
                    :max="fund.targetAmount * 1.5"
                    :min="0"
                    step="10"
                    class="mt-2"
                    thumb-label="always"
                    dense
                    @input="updateShortStatus(index)"
                  ></v-slider>
                  <div :class="{'text-red-500': fund.isShort, 'text-green-500': !fund.isShort}" class="caption">
                    {{ fund.isShort ? 'Shortfall: ' + formatCurrency(fund.targetAmount - fund.currentAmount) : 'On Track' }}
                  </div>
                </v-list-item-content>
              </v-list-item>
            </v-list> 
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script setup lang="ts">
  import { ref, computed } from 'vue';
  import { CurrencyFormatter } from '@/utilities/CurrencyFormatter';
  
  const { formatCurrency } = CurrencyFormatter();
  const funds = ref([
    {name: 'Rent', targetAmount: 2000, currentAmount: 1800, isShort: true},
    {name: 'Subscriptions', targetAmount: 350, currentAmount: 350, isShort: false},
    {name: 'Utilities', targetAmount: 150, currentAmount: 160, isShort: false},
    {name: 'Insurance', targetAmount: 312, currentAmount: 285, isShort: true},
    {name: 'Gas', targetAmount: 100, currentAmount: 100, isShort: false},
    {name: 'Food', targetAmount: 500, currentAmount: 450, isShort: true},
    {name: 'Entertainment', targetAmount: 250, currentAmount: 200, isShort: true},
    {name: 'Kids', targetAmount: 300, currentAmount: 310, isShort: false},
    {name: 'Vacation', targetAmount: 1200, currentAmount: 1300, isShort: false},
    {name: 'Debt', targetAmount: 750, currentAmount: 700, isShort: true}
]);
  
  const totalIncome = ref(4000);
  const updateShortStatus = (index: number) => {
    const fund = funds.value[index];
    fund.isShort = fund.currentAmount < fund.targetAmount;
  };
  
  const totalExpenses = computed(() => {
      return funds.value.reduce((total, fund) => total + fund.targetAmount, 0);
  });
  const totalSaved = computed(() => {
      return funds.value.reduce((total, fund) => total + fund.currentAmount, 0);
  });
  const net = computed(() => {
      return totalSaved.value - totalExpenses.value;
  });
  </script>
  
  <style>
  .text-red-500 {
    color: #F87171; /* Tailwind's red-500 */
  }
  .text-green-500 {
    color: #10B981; /* Tailwind's green-500 */
  }
  </style>
  