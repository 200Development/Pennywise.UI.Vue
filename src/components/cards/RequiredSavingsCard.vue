<script setup lang="ts">
import { ref } from 'vue';
import RequiredSavingsGraph from '../graphs/RequiredSavingsGraph.vue';

const cardTitle = ref('Required Savings');
</script>

<template>
    <v-card class="graphCard">
        <v-card-title class="text-center">{{ cardTitle }}</v-card-title>
        <v-card-text>
            <RequiredSavingsGraph></RequiredSavingsGraph>
        </v-card-text>
    </v-card>
</template>