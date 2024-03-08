<script setup>
import {ref} from 'vue'
const selectedFilter = ref('')
</script>

<template>
    <div class="order-report">
        <div class="title-and-filter">
            <h2 class="order-report__title">
                Order Report
            </h2>
            
            <select v-model="selectedFilter" class="selection" @change="">
                <option enabled value="">Filter Order</option>
                <option value="customer">Customer</option>
                <option value="menu">Menu</option>
                <option value="payment">Payment</option>
                <option value="status">Status</option>

            </select>
        </div>
    </div>
</template>


<style scoped lang="scss">
.order-report {
    width: 100%;
    background: var(--base-dark-bg-2);
    border-radius: 8px;
    height: 100%;
}

.title-and-filter {
    display: flex;
    margin-top: 24px;
    margin-left: 24px;
    margin-right: 16px;
    justify-content: space-between;
}

.order-report__title {
    font-family: 'Barlow';
    font-weight: 600;
    font-size: 20px;
    line-height: 140%;
    color: var(--white);
}

.order-report__filter-btn {
    display: flex;
    max-width: 125px;
    height: 45px;
    width: 100%;
    align-items: center;
    flex-direction: row;
    padding-left: 14px;
    background: var(--base-dark-bg-2);
    border: 1px solid var(--base-dark-line);
    border-radius: 8px;
    font-family: 'Barlow';
    font-weight: 500;
    font-size: 14px;
    line-height: 130%;
    color: var(--white);
    gap: 10px;
}

.selection {
    max-width: 125px;
    width: 125px;
    height: 45px;
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