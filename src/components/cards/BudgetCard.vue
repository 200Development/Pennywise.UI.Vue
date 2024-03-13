<script setup lang="ts">
import { ref } from 'vue';
import Budget from '@/components/Budget.vue';

const cardTitle = ref('Budget')
</script>

<template>
    <v-card>
        <v-card-title>{{ cardTitle }}</v-card-title>
        <v-card-text>
            <Budget></Budget>
        </v-card-text>
    </v-card>
</template>