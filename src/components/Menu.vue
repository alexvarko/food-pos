
<script setup>
import Header from './MenuHeader.vue'
import Dishes from './Dishes.vue'
import Order from './OrderBox.vue'

import { ref, onMounted, watch } from 'vue';

const orderTypeFromDishes = ref('dineIn');


watch(orderTypeFromDishes, (value) => {
    orderTypeFromDishes.value = value;
});


const dishesSelectedList = ref([]);
watch(dishesSelectedList, (value) => {
    dishesSelectedList.value = value;
});

</script>

<template>
    <div class="menu">
        <Header></Header>
        <Dishes v-model:orderType="orderTypeFromDishes" v-model:selectedDishes="dishesSelectedList"></Dishes>
    </div>
    <div class="order">
        <Order :orderTypeFromDishes="orderTypeFromDishes" :dishesSelectedList="dishesSelectedList"></Order>
    </div>
</template>

<style scoped>

.menu{
    width: 55%;
    padding: 24px 24px 0px 24px;
}

.order{
    display: flex;
    flex: 1;
    /* background-color: var(--base-dark-bg-2); */
}
</style> 