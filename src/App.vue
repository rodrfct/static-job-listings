<script setup lang="ts">
import { computed, ref, onMounted, onUnmounted } from 'vue';
import bgHeaderDesktop from './assets/images/bg-header-desktop.svg';
import bgHeaderMobile from './assets/images/bg-header-mobile.svg'
import ListingsSection from './components/ListingsSection.vue';

const windowSize = ref(window.innerWidth)

const bgHeader = computed(() => {
    if (windowSize.value < 450) {
        return bgHeaderMobile
    } else {
        return bgHeaderDesktop
    }
})

const getWindowSize = () => {
    windowSize.value = window.innerWidth
}

onMounted(() => {
    window.addEventListener('resize', getWindowSize)
})

onUnmounted(() => {
    window.removeEventListener('resize', getWindowSize)
})
</script>

<template>
  <img :src="bgHeader" alt="">
  <ListingsSection />
</template>

<style scoped>
img {
  width: 100%;
  background-color: var(--Desaturated-Dark-Cyan);
}
</style>
