<script setup>
import { ref, onMounted } from 'vue'

function getRandomInt(max) {
  return Math.floor(Math.random() * max);
}



const randomnumber = ref(null)
onMounted(() => {
  randomnumber.value = getRandomInt(1000)

})

defineProps(['orderTypeFromDishes'])

</script>


<template>
  <div class="container">
    <div class="container__inner">

      <div class="order__id">
        <h2 class="order__id-title">Orders #{{ randomnumber }}</h2>
      </div>

      <div class="order__type">
        <div class="order__type-btn" :class="{ 'order__type-btn--active': orderTypeFromDishes === 'dineIn' }">
          <p class="type-btn__name">
            Dine In
          </p>
        </div>
        <div class="order__type-btn" :class="{ 'order__type-btn--active': orderTypeFromDishes === 'toGo' }">
          <p class="type-btn__name">
            To Go
          </p>
        </div>
        <div class="order__type-btn" :class="{ 'order__type-btn--active': orderTypeFromDishes === 'delivery' }">
          <p class="type-btn__name">
            Delivery
          </p>
        </div>
      </div>

      <div class="headings">
        <div>
          <p>Item</p>
        </div>
        <div class="heading__qty-price">
          <p>Qty</p>
          <p>Price</p>
        </div>
      </div>
      <div class="selector-line"></div>

    </div>
  </div>
</template>



<style scoped>
.container {
  background-color: var(--base-dark-bg-2);
  height: 100%;
  width: 100%;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}

.container__inner {
  padding-left: 24px;
  padding-top: 24px;
  padding-right: 24px;
}

.order__id {
  padding-bottom: 24px;
}

.order__id-title {
  color: var(--white);
  font-family: "Barlow";
  font-size: 20px;
  font-weight: 600;
  line-height: 140%;
}

.order__type {
  display: flex;
  gap: 8px;
  padding-bottom: 24px;
}

.order__type-btn {
  min-width: 54px;
  height: 34px;
  border: 1px solid var(--base-dark-line);
  border-radius: 8px;
  color: var(--primary-color);

}

.type-btn__name {
  display: flex;
  padding: 7px 12px;
  justify-content: center;
  align-items: center;
  font-family: "Barlow";
  font-size: 14px;
  font-weight: 600;
  line-height: 140%;

}

.order__type-btn--active {
  background-color: var(--primary-color);
  color: var(--white);
  border: none;
}

.headings,
.headings div {
  display: flex;
  justify-content: space-between;
  color: var(--white);
  font-family: "Barlow";
  font-size: 16px;
  font-weight: 600;
  line-height: 140%;
}


.heading__qty-price {
  gap: 43px;
}

.selector-line {
  margin-top: 24px;
  height: 0.5px;
  background-color: var(--base-dark-line);
  opacity: 0.5;
  width: 100%;
  display: flex;


}
</style>