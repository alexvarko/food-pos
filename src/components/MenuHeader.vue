
<script setup>
import { ref, computed, onMounted } from 'vue'
import { useElementBounding } from '@vueuse/core'


const dateString = computed(() => {
    const date = new Date();
    const dayName = date.toLocaleDateString('en-us', { weekday: 'long' });
    const dayNum = date.getDay()
    const monthName = date.toLocaleDateString('en-us', { month: 'short' });
    const year = date.getFullYear()
    console.log("computed")
    return `${dayName}, ${dayNum} ${monthName} ${year}`
})

const hotDishes = ref(null);
    const coldDishes = ref(null);
    const soup = ref(null);
    const grill = ref(null);
    const appetizer = ref(null);
    const dessert = ref(null);

const menuCategories = ref([
    { id: 'hotDishes', Name: "Hot Dishes", isActive: true, ref: hotDishes },
    { id: 'coldDishes', Name: "Cold Dishes", isActive: false, ref: coldDishes },
    { id: 'soup', Name: "Soup", isActive: false, ref: soup  },
    { id: 'grill', Name: "Grill", isActive: false, ref: grill  },
    { id: 'appetizer', Name: "Appetizer", isActive: false , ref: appetizer },
    { id: 'dessert', Name: "Dessert", isActive: false , ref: dessert }
])

const activeElementX = ref(0)
const activeLineX = ref(0)
const cssVars = computed(()=>{return({'--leftX':activeLineX.value+"px"})})


const chooseActiveCategory = (category) => {
    // Set isActive for all categories to false
    menuCategories.value.forEach((item) => {
        item.isActive = false;
    });
    // Set isActive to true for the clicked category
    category.isActive = true;
    console.log(category.ref)
    activeElementX.value = useElementBounding(category.ref[0]).x.value
    activeLineX.value = activeElementX.value - 128;
}


</script>

<template>
    <div class="header">
        <div class="title-date">
            <h1 class="title">Jaegar Resto</h1>
            <h3 class="date">{{ dateString }}</h3>
        </div>
        <input type="text" class="header-input" placeholder="Search for food, coffe, etc..">
    </div>
    <div class="menu-selector">
        <div class="menu-selector__items">
            <p v-for="category in menuCategories" class="menu-categories" :class="{ 'active-category': category.isActive }" :ref="category.id"
                @click="chooseActiveCategory(category)">
                {{ category.Name }}
            </p>
        </div>
        <div class="selector-line" :style="cssVars"></div>

    </div>
</template>

<style scoped>

.title {
    color: var(--white);
    font-family: 'Barlow';
    font-size: 28px;
    font-style: normal;
    font-weight: 600;
    line-height: 39.2px;

}

.date {
    color: var(--text-lighter);
    font-family: 'Barlow';
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 22.4px;
}

.header {
    display: flex;
    justify-content: space-between;
    padding-bottom: 24px;
}

.header-input {
    width: 220px;
    height: 48px;
    background-color: var(--base-form-bg);
    border-radius: 8px;
    border: 1px solid var(--base-dark-line);
    background-image: url('../../static/header/search.svg');
    background-repeat: no-repeat;
    background-position: 14px;
    padding-left: 40px;
    color: var(--text-light);
}

.header-input:focus {
    outline: none;
}

.header-input::placeholder {
    color: var(--text-light);
    font-family: 'Barlow';
    font-size: 14px;
    font-style: normal;
    font-weight: 400;
    line-height: 140%;

}

.menu-selector {
    display: flex;
    flex-direction: column;
    padding-bottom: 24px;
}

.menu-selector__items {
    min-width: 481px;
    display: flex;
    align-items: flex-start;
    gap: 32px;
    padding-bottom: 13px;
}


.menu-selector__items p {
    font-family: 'Barlow';
    font-size: 15px;
    font-style: normal;
    font-weight: 600;
    line-height: 19.6px;
    left: var(--leftX);
}

.selector-line {
    height: 1px;
    background-color: var(--base-dark-line);
    width: 100%;
    display: flex;
    align-items: center;
    position: relative;
    transition: all .3s;

}
.selector-line::after{
    content: " ";
    position: absolute;
    height: 3px;
    width: 41px;
    border-radius: 6px;
    background-color: var(--primary-color);
    left: var(--leftX);
    transition: left 0.3s ease; 

}
.menu-categories{
    color: var(--white);
    transition: all .3s;
    cursor: pointer;
}

.menu-categories:not(.active-category):hover {
    color: var(--primary-color);
}
.active-category {
    color: var(--primary-color);

}
</style> 

















