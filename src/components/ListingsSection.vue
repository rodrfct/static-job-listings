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

    <div class="wrapper">
        <div v-show="activeFilters.length != 0" class="filter-display">
            <button v-for="filter in activeFilters" class="active-filter" type="button">
                <span class="text">{{ filter }}</span>
                <span @click="toggleActiveFilter(filter)" class="img">
                    <img src="../assets/icons/icon-remove.svg" alt="">
                </span>
            </button>

            <span @click="activeFilters = []" class="clear">Clear</span>
        </div>

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
    </div>

</template>

<style scoped>
.wrapper {
    margin-top: 50px;
    padding: 0 5%;
}

.wrapper ul {
    padding: 0;
}

.filter-display {
    background-color: white;
    color: var(--Desaturated-Dark-Cyan);
    padding: 20px;
    border-radius: 10px;

    box-shadow: 0px 5px 20px 2px #ddd;

    position: relative;
    top: -70px;
}

.filter-display .clear {
    text-decoration: underline;
    cursor: pointer;
    
    position: absolute;
    right: 5%;
    top: 45%;
}

.active-filter {
    border: none;
    outline: none;
    overflow: hidden;
    background-color: var(--Light-Grayish-Cyan-Filter-Tablets);
    
    padding: 0;
    margin: 4px 10px;
    border-radius: 7px;

    display: inline-flex;
    align-items: center;
}

.active-filter .text {
    color: var(--Desaturated-Dark-Cyan);
    font-weight: 700;
    
    padding: 7px;
}

.active-filter .img {
    background-color: var(--Desaturated-Dark-Cyan);
    padding: 5px 8px;

    cursor: pointer;
    transition: background-color .2s ease;
}

.active-filter .img:hover {
    background-color: var(--Very-Dark-Grayish-Cyan);
}

.active-filter .img img {
    width: 12px;
}

@media (width < 450px) {
    .filter-display .clear {
        text-decoration: none !important;
        color: var(--Dark-Grayish-Cyan);
        font-weight: 700;
    }
}
</style>