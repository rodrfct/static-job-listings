<script setup lang="ts">
import listingData from '../assets/data.json';
import Listing from './Listing.vue';

export interface ListingInterface {
    id: number
    company: string
    logo: string
    new: boolean
    featured: boolean
    position: string
    role: string
    level: string
    postedAt: string
    contract: string
    location: string
    languages: string[]
    tools: string[]
}
</script>

<template>
    <ul>
        <Listing v-for="listing in listingData" v-bind="listing" />
    </ul>
</template>

<style scoped>
ul {
    margin-top: 50px;
    padding: 0 5%;
}
</style>