<script setup>
import { ref, computed, onMounted, watch } from 'vue'
import { useElementBounding } from '@vueuse/core'
import GreyLine from '../common/GreyLine.vue'
import CurrentDate from '../common/CurrentDate.vue';

const hotDishes = ref(null);
const coldDishes = ref(null);
const soup = ref(null);
const grill = ref(null);
const appetizer = ref(null);
const dessert = ref(null);

const menuCategories = ref([
    { id: 'hotDishes', Name: "Hot Dishes", isActive: true, ref: hotDishes },
    { id: 'coldDishes', Name: "Cold Dishes", isActive: false, ref: coldDishes },
    { id: 'soup', Name: "Soup", isActive: false, ref: soup },
    { id: 'grill', Name: "Grill", isActive: false, ref: grill },
    { id: 'appetizer', Name: "Appetizer", isActive: false, ref: appetizer },
    { id: 'dessert', Name: "Dessert", isActive: false, ref: dessert }
])

const activeElementX = ref(0)
const activeLineX = ref()
const cssVars = computed(() => { return ({ '--leftX': activeLineX.value + "px" }) })


const chooseActiveCategory = (category) => {
    menuCategories.value.forEach((item) => {
        item.isActive = false;
    });
    category.isActive = true;
}

onMounted(() => {
    window.addEventListener('resize', handleWindowResize);
});

watch(menuCategories, (categories) => {
    const activeCategory = categories.find(category => category.isActive);
    if (activeCategory) {
        activeLineX.value = activeCategory.ref[0].offsetLeft;
    }
}, { deep: true });

const handleWindowResize = () => {
    const activeCategory = menuCategories.value.find(category => category.isActive);
    if (activeCategory) {
        activeLineX.value = activeCategory.ref[0].offsetLeft;
    }
}
</script>

<template>
    <div class="menu-selector">
        <div class="menu-selector__items">
            <p v-for="category in menuCategories" class="menu-categories"
                :class="{ 'active-category': category.isActive }" :ref="category.id"
                @click="chooseActiveCategory(category)">
                {{ category.Name }}
            </p>
        </div>
        <GreyLine :style="cssVars"></GreyLine>

    </div>
</template>

<style scoped>
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
    padding-left: 24px;
}


.menu-selector__items p {
    font-family: 'Barlow';
    font-size: 15px;
    font-style: normal;
    font-weight: 600;
    line-height: 19.6px;
    left: var(--leftX);
    position: relative;
}

.GreyLine {
    height: 1px;
    background-color: var(--base-dark-line);
    width: 100%;
    display: flex;
    align-items: center;
    position: relative;
    transition: all .3s;

}

.GreyLine::after {
    content: " ";
    position: absolute;
    height: 3px;
    width: 41px;
    border-radius: 6px;
    background-color: var(--primary-color);
    left: var(--leftX);
    transition: left 0.3s ease;

}

.menu-categories {
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

.selector-line {
    height: 1px;
    background-color: var(--base-dark-line);
    width: 100%;
    display: flex;
    align-items: center;
    position: relative;
    transition: all .3s;

}
</style>
