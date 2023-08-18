<script setup lang="ts">
import { ref } from 'vue';
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

const activeFilters = ref<string[]>([])

function toggleActiveFilter(filter: string): void {
    if (activeFilters.value.includes(<never>filter)) {
        activeFilters.value.splice(activeFilters.value.indexOf(<never>filter), 1)
    } else {
        activeFilters.value.push(<never>filter)
    }
}

function applyFilters(filters: string[], listing: ListingInterface): boolean {
    for (const element of filters) {
        if (
            listing.role != element &&
            listing.level != element &&
            !listing.languages.includes(element) &&
            !listing.tools.includes(element)
        ) {
            return false; // Element doesn't match
        }
    }
    return true; // All elements match
}
</script>

<template>
    <ul v-if="activeFilters.length == 0">
        <Listing v-for="listing in listingData"
         :key="listing.id"
         v-bind="listing"
         @toggle-filter="toggleActiveFilter"
        />
    </ul>

    <ul v-else>
        <template v-for="listing in listingData">
            <Listing v-if="applyFilters(activeFilters, listing)"
             :key="listing.id"
             v-bind="listing"
             @toggle-filter="toggleActiveFilter"
            />
        </template>
    </ul>

</template>

<style scoped>
ul {
    margin-top: 50px;
    padding: 0 5%;
}
</style>