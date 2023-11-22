
<script setup>
import { ref } from 'vue'
const selected = ref('')

</script>

<template>
    <div class="dish-chooser">
        <h2 class="title">Choose Dishes</h2>
        <select v-model="selected" class="selection">
            <option enabled value="">Dine In</option>
            <option>Dine Out</option>
            <option>Drinks</option>
        </select>
    </div>
</template>

<style scoped>
.dish-chooser {
    display: flex;
    justify-content: space-between;

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
</style> 