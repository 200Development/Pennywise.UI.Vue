<script setup lang="ts">
import NetWorthGraph from '../graphs/NetWorthGraph.vue';

const cardTitle = "Net Worth";
</script>

<template>
<v-card class="graphCard">
        <v-card-title class="text-center">{{ cardTitle }}</v-card-title>
        <v-card-text>
            <NetWorthGraph></NetWorthGraph>
        </v-card-text>
    </v-card>
</template>

<style scoped>
.graphCard {
    height: 400px;
}
</style>