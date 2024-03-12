<script setup lang="ts">
import { ref, computed } from 'vue';

const nextPayday = ref(new Date(2024, 2, 15)); // Note: Months are 0-indexed
const formattedNextPayday = computed(() => formatDate(nextPayday.value));

function formatDate(date: Date) {
    const options: Intl.DateTimeFormatOptions = { weekday: 'short', year: 'numeric', month: 'long', day: 'numeric' };
    return date.toLocaleDateString('en-US', options);
};
</script>

<template>
    <div>{{ formattedNextPayday }}</div>
</template>