<script setup lang="ts">
import type { ListingInterface } from './ListingsSection.vue';

const props = defineProps<ListingInterface>()
</script>

<template>
    <li class="listing"
     :style="{borderLeft: `${props.featured ? '5px solid var(--Desaturated-Dark-Cyan)' : '0px'}`}">
        <img :src="props.logo" alt="">

        <div class="info">
            <span id="company">{{ props.company }}</span>
            <span v-if="props.new" id="new">New!</span>
            <span v-if="props.featured" id="featured">Featured</span>

            <p>{{ props.position }}</p>

            <span>{{ props.postedAt }}</span>
            <span>{{ props.contract }}</span>
            <span>{{ props.location }}</span>
        </div>

        <div class="filters">
            <span>{{ props.role }}</span>
            <span>{{ props.level }}</span>

            <span v-for="lang in props.languages">{{ lang }}</span>
            <span v-for="tool in props.tools">{{ tool }}</span>
        </div>
    </li>
</template>

<style scoped>
.listing {
    background-color: white;
    border-radius: 5px;
    
    padding: 20px;
    margin: 15px auto;

    box-shadow: 0px 5px 20px 2px #ddd;

    display: grid;
    grid-template-rows: 1fr;
    grid-template-columns: auto 1fr auto;
    gap: 15px;
    align-items: center;
}

.listing img {
    width: 75px;
}

.info span {
    margin: auto 6px;
    color: var(--Dark-Grayish-Cyan);
}

.info p {
    font-size: 1.2em;
    font-weight: 700;
    color: var(--Very-Dark-Grayish-Cyan);

    margin-left: 6px;
}

.info span:nth-last-child(-n + 2)::before {
    content: "·";
    margin-right: 12px;
}

#company {
    color: var(--Desaturated-Dark-Cyan);
    font-weight: 700;
}

#new,
#featured {
    background-color: var(--Desaturated-Dark-Cyan);
    padding: 5px 8px;
    border-radius: 15px;

    color: white;
    text-transform: uppercase;
    font-weight: 700;
}

#featured {
    background-color: var(--Very-Dark-Grayish-Cyan);
}

.filters span {
    background-color: var(--Light-Grayish-Cyan-Filter-Tablets);
    color: var(--Desaturated-Dark-Cyan);
    font-weight: 700;
    
    padding: 7px;
    margin: 0 7px;
}
</style>