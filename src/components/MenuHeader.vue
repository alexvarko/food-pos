
<script setup>
import { ref, computed } from 'vue'


const dateString = computed(() => {
    const date = new Date();
    const dayName = date.toLocaleDateString('en-us', { weekday: 'long' });
    const dayNum = date.getDay()
    const monthName = date.toLocaleDateString('en-us', { month: 'short' });
    const year = date.getFullYear()
    console.log("computed")
    return `${dayName}, ${dayNum} ${monthName} ${year}`
})

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
            <p>Hot Dishes</p>
            <p>Cold Dishes</p>
            <p>Soup</p>
            <p>Grill</p>
            <p>Appetizer</p>
            <p>Dessert</p>
        </div>
        <div class="selector-line"><svg xmlns="http://www.w3.org/2000/svg" width="41" height="4" viewBox="0 0 41 4" fill="none">
<path d="M2 2H39" stroke="#EA7C69" stroke-width="3" stroke-linecap="round"/>
</svg></div></div>
   
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Barlow:wght@400;600&display=swap');

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
}

.menu-selector__items {
    min-width: 481px;
    display: flex;
    align-items: flex-start;
    gap: 32px;
    padding-bottom: 13px;
}


.menu-selector__items p {
    color: var(--white);
    font-family: 'Barlow';
    font-size: 15px;
    font-style: normal;
    font-weight: 600;
    line-height: 19.6px;
}

.selector-line {
    height: 1px;
    background-color: var(--base-dark-line);
    width: 100%;
    display: flex;
    align-items: center;
}


</style> 

















