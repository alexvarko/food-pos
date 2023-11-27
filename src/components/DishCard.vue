<script setup>
import { ref } from 'vue'
</script>

<template>
    <div class="container">
        <img class="dish-image" src="http://localhost:3001/dishes/1" alt="">
        <div class="infobox">
            <div class="textarea">
                <p class="dish__name">Spicy seasoned seafood noodles</p>
                <p class="dish__price">$ 2.29</p>
                <p class="dish__available">20 Bowls available</p>
            </div>

        </div>
    </div>
</template>

<style scoped>
.container {
    height: 260px;
    width: 192px;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.infobox {
    height: 226px;
    width: 100%;
    background-color: var(--base-dark-bg-2);
    position: absolute;
    bottom: 0;
    border-radius: 16px;
}

.dish-image {
    position: absolute;
    z-index: 1;
    transform: translateX(-50%);
    left: 50%;
}

.textarea{
    position: absolute;
    bottom: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 24px;
    justify-content: space-between;
    color: white;
    height: 88px;
}
</style>


