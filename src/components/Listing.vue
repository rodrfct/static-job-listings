<script setup lang="ts">
import type { ListingInterface } from './ListingsSection.vue';

const props = defineProps<ListingInterface>()

const emit = defineEmits(['toggle-filter'])

function toggleFilter(filter: string): void {
    emit('toggle-filter', filter)
}
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
            <span @click="toggleFilter(props.role)">{{ props.role }}</span>
            <span @click="toggleFilter(props.level)">{{ props.level }}</span>

            <span v-for="lang in props.languages"
             @click="toggleFilter(lang)">{{ lang }}</span>
            <span v-for="tool in props.tools"
             @click="toggleFilter(tool)">{{ tool }}</span>
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

    cursor: pointer;
    transition: color .2s ease;
}

.info p:hover {
    color: var(--Desaturated-Dark-Cyan);
}

.info span:nth-last-child(-n + 2)::before {
    content: "·";
    margin-right: 12px;
}

#company,
#new,
#featured {
    display: inline-block;
    font-weight: 700;
}

#company {
    color: var(--Desaturated-Dark-Cyan);
}

#new,
#featured {
    background-color: var(--Desaturated-Dark-Cyan);
    padding: 5px 8px;
    border-radius: 15px;

    color: white;
    text-transform: uppercase;
}

#featured {
    background-color: var(--Very-Dark-Grayish-Cyan);
}

.filters span {
    display: inline-block;

    background-color: var(--Light-Grayish-Cyan-Filter-Tablets);
    color: var(--Desaturated-Dark-Cyan);
    font-weight: 700;
    
    padding: 7px;
    margin: 7px;

    border-radius: 5px;

    cursor: pointer;
    transition: color .2s ease, background-color .2s ease;
}

.filters span:hover {
    background-color: var(--Desaturated-Dark-Cyan);
    color: white;
}

@media (width < 450px) {
    .listing {
        position: relative;
        grid-template-rows: 1fr 1fr;
        grid-template-columns: 100%;
        gap: 0;
        margin-bottom: 15%;
    }

    .listing img {
        width: 50px;
        position: absolute;
        top: 0;
        translate: 50% -50%;
    }

    .info {
        margin-top: 30px;
    }

    .filters {
        grid-row: 2;
        border-top: 1px solid var(--Dark-Grayish-Cyan);
        padding-top: 5px;
    }

}
</style>