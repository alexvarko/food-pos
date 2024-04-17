<script setup>
import GreyLine from '../common/GreyLine.vue'
import Chart from '../components/MostTypesChart.vue'
import { ref, onMounted } from 'vue'

const mostOrderedFilter = ref('today')
const mostOrderedList = ref(null)
const mostTypeFilter = ref('today')

onMounted(() => {
    setTimeout(() => {
        fetch('http://localhost:3001/most_ordered')
            .then(response => response.json())
            .then(data => mostOrderedList.value = data)
    }, 2000);
})
</script>

<template>
    <div class="dashboard-most-stats">
        <div class="most-ordered">
            <div class="most-ordered__heading">
                <h2 class="most-ordered__title">Most Ordered</h2>
                <select v-model="mostOrderedFilter" class="selection" @change=""
                    @click="{ mostOrderedFilter = mostOrderedFilter; console.log(mostOrderedFilter) }">
                    <option enabled value="today">Today</option>
                    <option value="lastMonth">Last Month</option>
                    <option value="lastYear">Last Year</option>
                </select>
            </div>
            <GreyLine></GreyLine>
            <div class="most-ordered__items">
                <div v-for="item in mostOrderedList" class="most-ordered__item">
                    <img :src="item.image" alt="" class="most-ordered__item--img">
                    <div class="most-ordered__item--info">
                        <p class="most-ordered__item--name">{{ item.name }}</p>
                        <p class="most-ordered__item--ordered">{{ item.ordered }} dishes ordered</p>
                    </div>

                </div>
            </div>
            <button class="view-all__btn">View All</button>
        </div>

        <div class="most-type">
            <div class="most-type__heading">
                <h2 class="most-type__title">Most Type of Order</h2>
                <select v-model="mostTypeFilter" class="selection" @change=""
                    @click="{ mostTypeFilter = mostTypeFilter; console.log(mostTypeFilter) }">
                    <option enabled value="today">Today</option>
                    <option value="lastMonth">Last Month</option>
                    <option value="lastYear">Last Year</option>
                </select>
            </div>
            <GreyLine></GreyLine>
            <Chart></Chart>
        </div>
    </div>
</template>

<style lang="scss" scoped>


.view-all__btn {
    position: absolute;
    bottom: 24px;
    /* Adjust the bottom margin as needed */
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    justify-content: center;
    align-items: center;
    width: calc(100% - 48px);
    height: 48px;
    border: 1px solid var(--primary-color);
    background-color: transparent;
    color: var(--primary-color);
    border-radius: 8px;
    font-family: 'Barlow';
    font-style: normal;
    font-weight: 600;
    font-size: 14px;
    line-height: 140%;
    transition: all .3s;
}

.view-all__btn:hover {
    cursor: pointer;
    height: 48px;
    border: 1px solid var(--red);
    background-color: transparent;
    color: var(--red);
}

.most-ordered__item--ordered {

    font-family: 'Barlow';
    font-style: normal;
    font-weight: 400;
    font-size: 12px;
    line-height: 140%;

    color: var(--text-light);


}

.most-ordered__item--name {

    font-family: 'Barlow';
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 130%;
    color: var(--text-lighter);
    margin-bottom: 4px;


}

.most-ordered__item--img {
    width: 56px;
    height: 56px;
    margin-right: 16px;
}

.most-ordered__item {
    display: flex;

}

.most-ordered__items {
    display: flex;
    flex-direction: column;
    margin-top: 20px;
    gap: 24px;
}

.dashboard-most-stats {
    height: auto;
    margin-top: 24px;
    margin-bottom: 24px;
    margin-right: 24px;
    position: relative;
    display: flex;
    flex-direction: column;
}



.most-ordered {
    position: relative;
    display: flex;
    flex-direction: column;
    height: 47%;
    width: 100%;
    background-color: var(--base-dark-bg-2);
    border-radius: 8px;
    padding: 24px;
    margin-bottom: 24px;

}

.most-type {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 100%;
    background-color: var(--base-dark-bg-2);
    border-radius: 8px;
    padding: 24px;
    flex: 1;

}

.most-ordered__heading {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}


.most-type__heading {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}

.most-ordered__title {
    font-family: 'Barlow';
    font-style: normal;
    font-weight: 600;
    font-size: 20px;
    line-height: 140%;
    color: var(--white);

}

.most-type__title {
    font-family: 'Barlow';
    font-style: normal;
    font-weight: 600;
    font-size: 20px;
    line-height: 140%;
    color: var(--white);

}



.selection {
    max-width: 125px;
    width: 125px;
    height: 47px;
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