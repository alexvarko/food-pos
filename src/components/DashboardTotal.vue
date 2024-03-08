<script setup>
import DashboardHeader from '../components/DashboardHeader.vue'
import TotalCard from './TotalCard.vue';
import OrderReport from './OrderReport.vue';

import { ref, onMounted } from 'vue'

const totalRevenue = ref(null)
const totalOrdered = ref(null)
const totalCustomers = ref(null)
onMounted(() => {
    setTimeout(() => {
        fetch('http://localhost:3001/total_revenue')
            .then(response => response.json())
            .then(data => totalRevenue.value = data)
        fetch('http://localhost:3001/total_ordered')
            .then(response => response.json())
            .then(data => totalOrdered.value = data)
        fetch('http://localhost:3001/total_customers')
            .then(response => response.json())
            .then(data => totalCustomers.value = data)
    }, 2000);


})
</script>

<template>
    <div class="dashboard-total">
        <DashboardHeader></DashboardHeader>
        <div class="total__cards" v-if="totalRevenue !== null && totalOrdered !== null && totalCustomers !== null">
            <TotalCard :imgUrl="'../../static/dashboard/coin.svg'" :totalStats="totalRevenue"></TotalCard>
            <TotalCard :imgUrl="'../../static/dashboard/order.svg'" :totalStats="totalOrdered"></TotalCard>
            <TotalCard :imgUrl="'../../static/dashboard/customer.svg'" :totalStats="totalCustomers"></TotalCard>
        </div>
        <div v-else class="loading">Loading...</div>
        <OrderReport v-if="totalRevenue !== null && totalOrdered !== null && totalCustomers !== null">></OrderReport>
    </div>
</template>

<style lang="scss" scoped>
.dashboard-total {
    width: 55%;
    margin: 24px 24px 24px 24px;
    display: flex;
    flex-direction: column;
}

.dashboard-header {
    margin-bottom: 24px;
}


.total__cards {
    display: flex;
    max-height: 145px;
    height: 100%;
    gap: 24px;
    margin-bottom: 24px;
}

.loading {

    color: var(--white);
    font-family: 'Barlow';
    font-size: 20px;
    font-style: normal;
    font-weight: 600;
    line-height: 140%;
}
</style>