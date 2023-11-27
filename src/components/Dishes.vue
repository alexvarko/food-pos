
<script setup>
import { ref, onMounted } from 'vue'
import DishCard from './DishCard.vue';
const selected = ref('dineIn')
const dishes = ref(null)
const getDishes = onMounted(() => {
    setTimeout(() => {
        fetch('http://localhost:3001/dishes')
        .then(response => response.json())
        .then(data => dishes.value = data)
    }, 3000);

})
</script>

<template>
    <div class="dish-chooser">
        <h2 class="title">Choose Dishes</h2>
        <select v-model="selected" class="selection">
            <option enabled value="dineIn">Dine In</option>
            <option value="dineOut">Dine Out</option>
            <option value="drinks">Drinks</option>
        </select>
    </div>
   <div class="dishes-container">
    <!-- <h3 v-if="!dishes" class="loading">Loading....</h3>
    <div v-else v-for="dish in dishes.data">{{dish}}</div> -->
    <DishCard></DishCard>
   </div>
</template>

<style scoped>
.dish-chooser {
    display: flex;
    justify-content: space-between;
    padding-bottom: 24px;
}

.title {
    color: var(--white);
    font-family: Barlow;
    font-size: 20px;
    font-style: normal;
    font-weight: 600;
    line-height: 140%;
}

.selection {
    display: inline-flex;
    padding: 14px;
    align-items: center;
    gap: 10px;
    border-radius: 8px;
    border: 1px solid #393C49;
    background: #1F1D2B;
    color: var(--white);
    font-family: 'Barlow';
    font-size: 14px;
    font-style: normal;
    font-weight: 500;
    line-height: 130%;
    width: 100px;
    direction: rtl;
    appearance: none;
    background-image: url(../../static/header/arrow-down.svg);
    background-size:
        20px 20px,
        20px 20px;
    background-position:
        calc(14px),
        calc(14px),
        100% 0;
    background-repeat: no-repeat;
}

select.selection:focus {
    outline: none;
}

.dishes-container{
    height: 100%;
}
</style> 