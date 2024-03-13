<script setup lang="ts">
import { SinkingFundsModel } from '@/models/SinkingFundsModel';
import SinkingFundsList from '@/components/SinkingFundsList.vue';
import { ref } from 'vue';
import SinkingFundsAdditionalDetailsCard from './SinkingFundsAdditionalDetailsCard.vue';


const cardTitle = "Sinking Funds";
const selectedFund = ref<SinkingFundsModel>();

function fundSelected(fund: SinkingFundsModel) {
 selectedFund.value = fund;
};
</script>

<template>
 <v-card>
        <v-card-title class="text-center">{{ cardTitle }}</v-card-title>
        <v-card-text>
            <v-row>
                <v-col cols="6" class="sinking-fund-list">
                    <SinkingFundsList @fund-selected="fundSelected"></SinkingFundsList>
                </v-col>
                <v-col cols="6">
                    <SinkingFundsAdditionalDetailsCard :fund="selectedFund"></SinkingFundsAdditionalDetailsCard>
                </v-col>
            </v-row>
        </v-card-text>
    </v-card>
</template>

<style>
.sinking-fund-list {
    min-height: 390px;
}
</style>