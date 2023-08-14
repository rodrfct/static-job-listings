<script setup lang="ts">
import type { ListingInterface } from './ListingsSection.vue';

const props = defineProps<ListingInterface>()
</script>

<template>
    <li>
        <img :src="props.logo" alt="">

        <div>{{ props.id }}</div>
        <div>{{ props.company }}</div>
        <div>{{ props.role }}</div>
        <div>{{ props.level }}</div>
        <div>{{ props.postedAt }}</div>
        <div>{{ props.location }}</div>
        <div>{{ props.contract }}</div>
        <div>{{ props.featured }}</div>
        <div>{{ props.languages }}</div>
        <div>{{ props.new }}</div>
        <div>{{ props.location }}</div>
        <div>{{ props.tools }}</div>
    </li>
</template>