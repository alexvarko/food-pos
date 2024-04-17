
<script setup>
import DashboardTotal from '../components/DashboardTotal.vue'
import DashboardMostStats from '../components/DashboardMostStats.vue';
</script>

<template>
    <DashboardTotal></DashboardTotal>
    <DashboardMostStats></DashboardMostStats>
</template>


<style scoped lang="scss">

.dashboard-total{
    width: 55%;
}

.dashboard-most-stats{
    display: flex;
    flex: 1;

}
</style>