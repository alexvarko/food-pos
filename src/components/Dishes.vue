
<script setup>
import {ref} from 'vue'
const test = ref(['dsad', 'dsd'])
</script>

<template>
    <div class="dish-chooser">
        <h2 class="title">Choose Dishes</h2>
        <select  name="" id=""></select>
    </div>
</template>

<style scoped>
.dish-chooser{
    display: flex;
    justify-content: space-between;
    
}
.title{
    color: var(--white);
font-family: Barlow;
font-size: 20px;
font-style: normal;
font-weight: 600;
line-height: 140%; /* 28px */
}

</style> 