<script setup>
import { ref, defineProps } from 'vue'
defineProps(['dish'])
</script>

<template>
    <div class="dish-card">
        <img class="dish-image" :src="dish.image" alt="">
        <div class="infobox">
            <div class="textarea">
                <p class="dish__name">{{dish.name}}</p>
                <p class="dish__price">$ {{dish.price}}</p>
                <p class="dish__available">{{dish.available}} Bowls available</p>
            </div>

        </div>
    </div>
</template>

<style scoped>
.dish-card {
    min-height: 260px;
    width: 192px;
    position: relative;
    display: flex;
    flex-direction: column;
    margin-bottom: 24px;
    cursor: pointer;
}

.infobox {
    height: 226px;
    width: 100%;
    background-color: var(--base-dark-bg-2);
    position: absolute;
    bottom: 0;
    border-radius: 16px;
    display: flex;
    justify-content: center;
}

.dish-image {
    position: absolute;
    z-index: 1;
    transform: translateX(-50%);
    left: 50%;
}

.textarea {

    width: 144px;
    position: absolute;
    bottom: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    margin-bottom: 24px;
    justify-content: space-between;
    height: 88px;
}

.dish__name {
    color: var(--white);
    text-align: center;
    font-family: 'Barlow';
    font-size: 14px;
    font-style: normal;
    font-weight: 500;
    line-height: 130%;
}

.dish__price {
    color: var(--white);
    text-align: center;
    font-family: 'Barlow';
    font-size: 14px;
    font-style: normal;
    font-weight: 400;
    line-height: 140%;
}

.dish__available {
    color: var(--text-light);
    text-align: center;
    font-family: 'Barlow';
    font-size: 14px;
    font-style: normal;
    font-weight: 400;
    line-height: 140%;
}
</style>


