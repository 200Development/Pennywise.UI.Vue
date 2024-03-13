<script setup lang="ts">
import ExpensesTreemapGraph from '../graphs/ExpensesTreemapGraph.vue';

const cardTitle = "Expenses Treemap";
</script>

<template>
    <v-card class="graphCard">
        <v-card-title class="text-center">{{ cardTitle }}</v-card-title>
        <v-card-text>
            <ExpensesTreemapGraph></ExpensesTreemapGraph>
        </v-card-text>
    </v-card>
</template>

<style scoped>
.graphCard {
  height: 400px;
}
</style>