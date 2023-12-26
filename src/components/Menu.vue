
<script setup>
import Header from './MenuHeader.vue'
import Dishes from './Dishes.vue'
import Order from './OrderBox.vue'

import { ref, onMounted, watch } from 'vue';

const orderTypeFromDishes = ref('dineIn');


watch(orderTypeFromDishes, (value) => {
    orderTypeFromDishes.value = value;
});

</script>

<template>
    <div class="menu">
        <Header></Header>
        <Dishes v-model="orderTypeFromDishes"></Dishes>
    </div>
    <div class="order">
        <Order :orderTypeFromDishes="orderTypeFromDishes"></Order>
    </div>
</template>

<style scoped>

.menu{
    min-width: 633px;
    width: 60%;
    padding: 24px 24px 0px 24px;
}

.order{
    display: flex;
    flex: 1;
    
}
</style> 