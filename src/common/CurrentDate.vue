<template>
    <h3 class="date">{{ dateString }}</h3>
</template>

<script setup>
import { computed } from 'vue'

const dateString = computed(() => {
    const date = new Date();
    const dayName = date.toLocaleDateString('en-us', { weekday: 'long' });
    const dayNum = date.getDay()
    const monthName = date.toLocaleDateString('en-us', { month: 'short' });
    const year = date.getFullYear()
    return `${dayName}, ${dayNum} ${monthName} ${year}`
})
</script>

<style lang="scss" scoped>
.date {
    color: var(--text-lighter);
    font-family: 'Barlow';
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 22.4px;
}
</style>