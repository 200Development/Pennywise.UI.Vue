
<script setup lang='ts'>
import { onMounted, ref } from 'vue';

const items = ref([
    { 'Sinking_Fund': 'Groceries', 'Required_Savings': 55.25, 'Current_Savings': 50.00 },
    { 'Sinking_Fund': 'Rent', 'Required_Savings': 600.00, 'Current_Savings': 550.00 },
    { 'Sinking_Fund': 'Gas', 'Required_Savings': 100.00, 'Current_Savings': 75.00 },
    // Add more items as needed
]);

const headers = ref([
    { title: 'Sinking Fund', value: 'Sinking_Fund' }, // The 'value' matches the item object keys
    { title: 'Required Savings', value: 'Required_Savings' },
    { title: 'Current Savings', value: 'Current_Savings' },
    { title: '+/-', value: 'Difference' }, // Define a header for the difference
]);


</script>

<template>
    <v-data-table :headers="headers" :items="items">
       <template v-slot:item.Sinking_Fund="{ item }">
            {{ item['Sinking_Fund'] }}
        </template>
        <!-- Slot for Required Savings -->
        <template v-slot:item.Required_Savings="{ item }">
            ${{ item['Required_Savings'].toFixed(2) }}
        </template>
        
        <!-- Slot for Current Savings -->
        <template v-slot:item.Current_Savings="{ item }">
            ${{ item['Current_Savings'].toFixed(2) }}
        </template>
        
        <!-- Slot for displaying the calculated difference -->
        <!-- Since you're calculating it on the fly, ensure the header value matches what's expected here -->
        <template v-slot:item.Difference="{ item }">
            ${{ (item['Required_Savings'] - item['Current_Savings']).toFixed(2) }}
        </template>
    </v-data-table>
</template>
  