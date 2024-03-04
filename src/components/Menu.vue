
<script setup>
import Header from './MenuHeader.vue'
import Dishes from './Dishes.vue'
import Order from './OrderBox.vue'

import { ref, onMounted, watch } from 'vue';

const orderTypeFromDishes = ref('dineIn');

const paymentEnable = ref(false)

watch(orderTypeFromDishes, (value) => {
    orderTypeFromDishes.value = value;
});


const dishesSelectedList = ref([]);
watch(dishesSelectedList, (value) => {
    dishesSelectedList.value = value;
});



</script>

<template>
    <div class="menu" :class="{'eclipse':paymentEnable}">
        <Header></Header>
        <Dishes v-model:orderType="orderTypeFromDishes" v-model:selectedDishes="dishesSelectedList"></Dishes>
    </div>
    <div class="order">
        <Order :orderTypeFromDishes="orderTypeFromDishes" :dishesSelectedList="dishesSelectedList" @update:orderPaymentEnable="paymentEnable = $event"></Order>
    </div>
</template>

<style scoped>

.menu{
    width: 55%;
    padding: 24px 24px 0px 24px;
}

.eclipse::after{
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: black;
    opacity: 0.7;
    z-index: 1;
}

.order{
    display: flex;
    flex: 1;
    /* background-color: var(--base-dark-bg-2); */
}
</style> 