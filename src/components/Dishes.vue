
<script setup>
import { ref, onMounted, defineEmits } from 'vue'
import DishCard from './DishCard.vue';
const dishes = ref(null)
const dishesContainer = ref(null);

const calculateMaxHeight = () => {
    if (dishesContainer.value) {
        const windowHeight = window.innerHeight;
        const containerTopOffset = dishesContainer.value.getBoundingClientRect().top;
        const calculatedMaxHeight = windowHeight - containerTopOffset - /* Add additional offset if needed */ 16;
        dishesContainer.value.style.maxHeight = `${calculatedMaxHeight + 20}px`;
    }
};
onMounted(() => {
    setTimeout(() => {
        fetch('http://localhost:3001/dishes')
            .then(response => response.json())
            .then(data => dishes.value = data)
    }, 2000);
    calculateMaxHeight(); // Calculate initially
    window.addEventListener('resize', calculateMaxHeight);

})

const props = defineProps(['orderType', 'selectedDishes']);
const emits = defineEmits();

const selected = ref("dineIn");
const dishesSelectedList = ref([])

const emitSelected = () => {
    emits('update:orderType', selected.value);
};

const addDish = (dish) => {
    const index = dishesSelectedList.value.findIndex(item => item.id === dish.id);

    if (index !== -1) {
        dishesSelectedList.value[index].amount++;
    } else {
        dishesSelectedList.value.push({ ...dish, amount: 1, description: ""  });
    }

    emits('update:selectedDishes', dishesSelectedList.value);
}

</script>

<template>
    <div class="dish-chooser">
        <h2 class="title">Choose Dishes</h2>
        <select v-model="selected" class="selection" @change="emitSelected">
            <option enabled value="dineIn">Dine In</option>
            <option value="toGo">To Go</option>
            <option value="delivery">Delivery</option>
        </select>
    </div>
    <div class="dishes-container" ref="dishesContainer">
        <h3 v-if="!dishes" class="loading">Loading....</h3>
        <DishCard v-else v-for="dishitem in dishes.data" :dish="dishitem" :key="dishitem.id" @click="addDish(dishitem)">{{ dish }}</DishCard>
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
    border: 1px solid var(--base-dark-line);
    background: var(--base-dark-bg-2);
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

.dishes-container {
    gap: 10px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    overflow-y: auto;
    overflow-x: hidden;

}

.dishes-container::-webkit-scrollbar {
    display: none;
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