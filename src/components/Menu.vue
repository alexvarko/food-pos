
<script setup>
import Header from './MenuHeader.vue'
import Dishes from './Dishes.vue'
</script>

<template>
    <div class="menu">
        <Header></Header>
        <Dishes></Dishes>
    </div>
</template>

<style scoped>

.menu{
    min-width: 633px;
    width: 60%;
    padding: 24px 24px 0px 24px;
}

</style> 