<script setup>
import {ref} from 'vue'
import ManagementSelectionLine from '../components/ManagementSelectionLine.vue'
import ManageDishes from './ManageDishes.vue';
const selectedFilter = ref('manage-categories')
</script>

<template>
    <div class="container">
        <div class="title-and-filter">
            <h2 class="title">
                Products Management
            </h2>
            <select v-model="selectedFilter" class="selection" @change=""
                @click="{ selectedFilter = selectedFilter; console.log(selectedFilter) }">
                <option enabled value="manage-categories">Manage Categories</option>
                <option value="manage-dishes">Manage Dishes</option>
                <option value="manage-drinks">Manage Drinks</option>
            </select>
        </div>
        <ManagementSelectionLine></ManagementSelectionLine>
        <ManageDishes v-model:orderType="orderTypeFromDishes" v-model:selectedDishes="dishesSelectedList"></ManageDishes>
    </div>
</template>

<style scoped>

.container{
    flex: 1;
    margin-top: 86px;
    margin-bottom: 24px;
    margin-right: 24px;
    background-color: var(--base-dark-bg-2);
    border-radius: 8px;
    position: relative;
}


.title-and-filter {
    display: flex;
    margin: 24px;
    justify-content: space-between;
}

.title {
    font-family: 'Barlow';
    font-weight: 600;
    font-size: 20px;
    line-height: 140%;
    color: var(--white);
}

.selection {
    width: 178px;
    height: 48px;
    display: flex;
    padding: 14px;
    align-items: center;
    gap: 10px;
    border-radius: 8px;
    border: 1px solid var(--base-dark-line);
    background: var(--base-dark-bg-2);
    color: var(--white);
    font-family: 'Barlow';
    font-size: 14px;
    font-style: normal;
    font-weight: 500;
    line-height: 130%;
    direction: rtl;
    appearance: none;
    background-image: url(../../static/dashboard/filter.svg);
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
</style>