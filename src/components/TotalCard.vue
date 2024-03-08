<template>
    <div class="total-card">
        <div class="first-row">
            <div class="image-box">
                <img :src="imgUrl" alt="">
            </div>
            <div class="percentage">
                <p :class="[totalStats.percentage > 0 ? 'percentage-positive' : 'percentage-negative']">
                    {{ (totalStats.percentage < 0 ? "" : "+") + totalStats.percentage.toFixed(2) }}% </p>
                        <svg v-if="totalStats.percentage > 0" width="18" height="18" viewBox="0 0 18 18" fill="none"
                            xmlns="http://www.w3.org/2000/svg">
                            <rect width="18" height="18" rx="9" fill="#88E091" fill-opacity="0.24" />
                            <path
                                d="M8.99994 14.25C8.75473 14.25 8.55208 14.0704 8.52 13.8375L8.51558 13.7727L8.51583 5.38275L5.45258 8.4139C5.26384 8.60069 4.95716 8.60134 4.7676 8.41535C4.59528 8.24628 4.57906 7.98116 4.71935 7.79402L4.76613 7.74039L8.65645 3.89039L8.66665 3.88095C8.67711 3.87118 8.68801 3.86186 8.69932 3.85302L8.65645 3.89039C8.67519 3.87184 8.6951 3.85513 8.71594 3.84025C8.72903 3.83126 8.74262 3.82253 8.75666 3.81448C8.7879 3.79629 8.82059 3.7822 8.85421 3.7718C8.86606 3.7683 8.87816 3.76504 8.89044 3.76225C8.89982 3.75997 8.90934 3.7581 8.91891 3.75652C8.92928 3.75493 8.93965 3.75355 8.95012 3.75249C8.96063 3.7513 8.97138 3.75057 8.98213 3.75018C8.98809 3.7501 8.994 3.75 8.99994 3.75L9.01602 3.75014C9.02795 3.75054 9.03986 3.75136 9.05174 3.75262L8.99994 3.75C9.02759 3.75 9.05471 3.75229 9.0811 3.75667C9.09313 3.75863 9.1052 3.76112 9.11719 3.76406C9.12671 3.76641 9.13606 3.76901 9.14529 3.77187C9.15626 3.77524 9.16731 3.77909 9.17823 3.78336C9.18951 3.78778 9.20053 3.79257 9.21133 3.79774C9.2196 3.80165 9.22812 3.80604 9.23653 3.81069C9.25231 3.81946 9.26712 3.82875 9.28135 3.83878C9.28358 3.84036 9.28604 3.84212 9.28848 3.84392C9.3101 3.85984 9.32917 3.87633 9.34683 3.89419L13.2338 7.74036C13.4226 7.92713 13.422 8.22933 13.2324 8.41533C13.0601 8.58442 12.791 8.59927 12.6017 8.46025L12.5474 8.41393L9.48475 5.38333L9.48429 13.7727C9.48429 14.0363 9.26744 14.25 8.99994 14.25Z"
                                fill="#50D1AA" />
                        </svg>
                        <svg v-else width="18" height="18" viewBox="0 0 18 18" fill="none"
                            xmlns="http://www.w3.org/2000/svg">
                            <rect width="18" height="18" rx="9" fill="#FF6471" fill-opacity="0.24" />
                            <path
                                d="M9.00006 3.75C9.24527 3.75 9.44792 3.92955 9.48 4.16251L9.48442 4.22727L9.48417 12.6172L12.5474 9.5861C12.7362 9.39931 13.0428 9.39866 13.2324 9.58465C13.4047 9.75372 13.4209 10.0188 13.2807 10.206L13.2339 10.2596L9.34355 14.1096L9.33335 14.119C9.32289 14.1288 9.31199 14.1381 9.30068 14.147L9.34355 14.1096C9.32481 14.1282 9.3049 14.1449 9.28406 14.1597C9.27097 14.1687 9.25738 14.1775 9.24334 14.1855C9.2121 14.2037 9.17941 14.2178 9.14579 14.2282C9.13394 14.2317 9.12184 14.235 9.10956 14.2378C9.10018 14.24 9.09066 14.2419 9.08109 14.2435C9.07072 14.2451 9.06035 14.2465 9.04988 14.2475C9.03937 14.2487 9.02862 14.2494 9.01787 14.2498C9.01191 14.2499 9.006 14.25 9.00006 14.25L8.98398 14.2499C8.97205 14.2495 8.96014 14.2486 8.94826 14.2474L9.00006 14.25C8.97241 14.25 8.94529 14.2477 8.9189 14.2433C8.90687 14.2414 8.8948 14.2389 8.88281 14.2359C8.87329 14.2336 8.86394 14.231 8.85471 14.2281C8.84374 14.2248 8.83269 14.2209 8.82177 14.2166C8.81049 14.2122 8.79947 14.2074 8.78867 14.2023C8.7804 14.1983 8.77188 14.194 8.76347 14.1893C8.74769 14.1805 8.73288 14.1712 8.71865 14.1612C8.71642 14.1596 8.71396 14.1579 8.71152 14.1561C8.6899 14.1402 8.67083 14.1237 8.65317 14.1058L4.76616 10.2596C4.5774 10.0729 4.57803 9.77067 4.76757 9.58467C4.93989 9.41558 5.209 9.40073 5.39832 9.53975L5.45255 9.58607L8.51525 12.6167L8.51571 4.22727C8.51571 3.96368 8.73256 3.75 9.00006 3.75Z"
                                fill="#FF7CA3" />
                        </svg>
            </div>
        </div>
        <div class="second-row">
            <h1 class="total-value">
                {{ (totalStats.name == 'revenue' ? '$' : '') + totalStats.amount.toLocaleString('en-US',
                    { maximumFractionDigits: 2 }) }}
            </h1>
            <p class="total-title">{{ totalTitle[totalStats.name] }}</p>
        </div>


    </div>
</template>


<script setup>
import { ref } from 'vue'
const props = defineProps(['imgUrl', 'totalStats'])
const imgUrl = props.imgUrl
const totalStats = props.totalStats
const totalTitle = { "revenue": "Total Revenue", "ordered": "Total Dish Ordered", "customers": "Total Customers" }
</script>

<style lang="scss" scoped>
.total-card {
    padding: 16px 16px 16px 16px;
    width: 100%;
    height: 100%;
    background-color: var(--base-dark-bg-2);
    border-radius: 8px;
}

.image-box {
    background: var(--base-dark-bg-1);
    border-radius: 8px;
    padding: 10px;
    max-width: fit-content;
    max-height: fit-content;
    display: flex;
    justify-content: center;
    margin-right: 12px;
}

.first-row {
    display: flex;
    margin-bottom: 8px;
}

.percentage {
    display: flex;
    align-items: center;
    justify-content: center;
}

.percentage-positive {

    font-family: 'Barlow';
    font-weight: 500;
    font-size: 12px;
    line-height: 140%;
    color: var(--green);
    margin-right: 6px;

}

.percentage-negative {

    font-family: 'Barlow';
    font-weight: 500;
    font-size: 12px;
    line-height: 140%;
    color: var(--red);
    margin-right: 6px;

}

.total-value {

    font-family: 'Barlow';
    font-weight: 600;
    font-size: 28px;
    line-height: 140%;
    color: var(--white);
    margin-bottom: 8px;

}

.total-title{

font-family: 'Barlow';
font-weight: 500;
font-size: 14px;
line-height: 130%;

color: var(--text-light);

}
</style>

