<script setup>
import GreyLine from '../common/GreyLine.vue'
import CurrentDate from '../common/CurrentDate.vue';

</script>

<template>
    <div class="dashboard-header">
    <div class="header">
        <div class="title-date">
            <h1 class="title">Dashboard</h1>
            <CurrentDate></CurrentDate>
        </div>
        
    </div>
    <GreyLine></GreyLine>
</div>
</template>

<style lang="scss" scoped>
.title {
    color: var(--white);
    font-family: 'Barlow';
    font-size: 28px;
    font-style: normal;
    font-weight: 600;
    line-height: 39.2px;

}

.header {
    display: flex;
    justify-content: space-between;
    padding-bottom: 24px;
}
</style>