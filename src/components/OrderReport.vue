<script setup>
import GreyLine from '../common/GreyLine.vue'

import { ref, onMounted } from 'vue'
const selectedFilter = ref('')

const orderReportItems = ref(null)

onMounted(() => {
    setTimeout(() => {
        fetch('http://localhost:3001/order_report')
            .then(response => response.json())
            .then(data => orderReportItems.value = data)
    }, 2000);
})

</script>

<template>
    <div class="order-report">
        <div class="title-and-filter">
            <h2 class="order-report__title">
                Order Report
            </h2>
            <select v-model="selectedFilter" class="selection" @change=""
                @click="{ selectedFilter = selectedFilter; console.log(selectedFilter) }">
                <option enabled value="">Filter Order</option>
                <option value="customer">Customer</option>
                <option value="menu">Menu</option>
                <option value="payment">Payment</option>
                <option value="status">Status</option>
            </select>
        </div>
        <div class="order-report__table">
            <div class="table-head">
                <div class=" table-row-title">
                    <div>Customer</div>
                    <div>Menu</div>
                    <div>Total Payment</div>
                    <div>Status</div>
                </div>
                <GreyLine></GreyLine>
            </div>
            <div class="table-content">
                <div class="table-row-content" v-if="orderReportItems" v-for="item in orderReportItems" :key="item.id">
                    <div class="item-cell customer-image-name-item"><img :src="item.image" alt="">
                        <p>{{ item.customer }}</p>
                    </div>
                    <div class="item-cell customer-menu-item">
                        <p>{{ item.menu }}</p>
                    </div>
                    <div class="item-cell">
                        <p>${{ item.total_payment }}</p>
                    </div>
                    <div class="item-cell status" :class="item.status">
                        <p>{{ item.status }}</p>
                    </div>
                </div>

                <div v-else class="loading">Loading...</div>
            </div>


        </div>
    </div>
</template>


<style scoped lang="scss">

.loading {

color: var(--white);
font-family: 'Barlow';
font-size: 20px;
font-style: normal;
font-weight: 600;
line-height: 140%;
margin-left: 24px;
}

.status {

    max-width: 91px;
    max-height: 26px;
    padding: 4px 12px;
    gap: 10px;
    border-radius: 30px;
    display: flex;
    justify-content: center;

    font-family: 'Barlow';
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 130%;



}

.Completed {
    color: var(--green);
    background: rgba(107, 226, 190, 0.24);
}

.Preparing {
    color: var(--purple);
    background: rgba(146, 144, 254, 0.2);

}

.Pending {
    color: #FFB572;
    background: rgba(255, 181, 114, 0.2);

}

.order-report {
    width: 100%;
    background: var(--base-dark-bg-2);
    border-radius: 8px;
    height: 100%;
    display: flex;
    flex-direction: column;
}

.title-and-filter {
    display: flex;
    margin-top: 24px;
    margin-left: 24px;
    margin-right: 16px;
    margin-bottom: 16px;
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

.order-report__table {
    display: flex;
    flex-direction: column;
    flex: 1;
    overflow: auto;


}

.table-head {
    grid-column: span 4; // Span all 4 columns

    font-family: 'Barlow';
    font-weight: 600;
    font-size: 14px;
    line-height: 140%;
    color: var(--white);
    max-height: 46px;
    margin-bottom: 16px;


}



.table-row-content {
    display: grid;
    grid-template-columns: 25% 25% 25% 25%; // Use fractional units to distribute columns equally
    padding-left: 24px;
    font-family: 'Barlow';
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 140%;
    color: var(--text-lighter);
    height: 100%;
}

.item-cell {}

.table-row-title {
    display: grid;
    grid-template-columns: 25% 25% 25% 25%; // Use fractional units to distribute columns equally
    max-height: 46px;
    padding-left: 24px;
    margin-bottom: 16px;


}


.table-content {
    display: flex;
    flex-direction: column;
    height: 100%;
    flex: 1;
    overflow-y: auto;
    overflow-x: hidden;


}

.customer-image-name-item {
    display: flex;

    img {
        height: 32px;
        width: 32px;
    }

    gap: 16px;

}

.customer-menu-item {
    p {
        display: flex;
        max-width: 137px;
    }
}
</style>