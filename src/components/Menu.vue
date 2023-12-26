
<script setup>
import Header from './MenuHeader.vue'
import Dishes from './Dishes.vue'
import Order from './OrderBox.vue'
</script>

<template>
    <div class="menu">
        <Header></Header>
        <Dishes></Dishes>
    </div>
    <div class="order">
        <Order></Order>
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