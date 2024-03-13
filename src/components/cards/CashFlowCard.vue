<script setup lang="ts">
import CashFlowGraph from '../graphs/CashFlowGraph.vue';
const cardTitle = "Cash Flow";
</script>

<template>
    <v-card class="graphCard">
        <v-card-title class="text-center">{{ cardTitle }}</v-card-title>
        <v-card-text>
            <CashFlowGraph></CashFlowGraph>
        </v-card-text>
    </v-card>
</template>

<style scoped>
.graphCard {
    height: 400px;
}
</style>