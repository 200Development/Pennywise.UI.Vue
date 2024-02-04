<script setup lang="ts">
import { ref, computed } from 'vue';

const links = ref([
    'Home',
    'About Us',
    'Contact Us',
]);

const currentYear = computed(() => new Date().getFullYear());
</script>

<template>
    <v-footer color="primary lighten-1" padless>
        <v-row justify="center" no-gutters>
            <v-btn v-for="link in links" :key="link" color="white" text rounded class="my-2">
                {{ link }}
            </v-btn>
            <v-col class="primary lighten-2 py-4 text-center white--text" cols="12">
                {{ currentYear }} — <strong>Pennywise</strong>
            </v-col>
        </v-row>
    </v-footer>
</template>