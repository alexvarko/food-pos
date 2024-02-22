<script setup>
import { ref, onMounted, watch } from 'vue'
import SelectedDish from './SelectedDish.vue'
function getRandomInt(max) {
  return Math.floor(Math.random() * max);
}



const randomnumber = ref(null)
onMounted(() => {
  randomnumber.value = getRandomInt(1000)

})

const props = defineProps(['orderTypeFromDishes', "dishesSelectedList"])


const totalSum = () => props.dishesSelectedList.reduce((sum, dish) => {
  return sum + (dish.price * dish.amount);
}, 0)

watch(totalSum, (value) => {
  totalSum.value = value;
});
</script>


<template>
  <div class="container">
    <div class="container__inner">

      <div class="order__id">
        <h2 class="order__id-title">Orders #{{ randomnumber }}</h2>
      </div>

      <div class="order__type">
        <div class="order__type-btn" :class="{ 'order__type-btn--active': orderTypeFromDishes === 'dineIn' }"
          @click="selectedDishes">
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
      <div class="selected-dishes">
        <h3 v-if="!dishesSelectedList.length" class="loading selected-dishes-empty">Select Dish to order</h3>
        <SelectedDish v-else v-for="dish in dishesSelectedList" :selectedDish="dish"></SelectedDish>
      </div>
      <div class="selector-line"></div>
      <div class="total">
        <div class="discount">
          <p class="total__title">Discount</p>
          <p class="total__value">$0</p>
        </div>
        <div class="sum">
          <p class="total__title">Sub total</p>
          <p class="total__value">$ {{ totalSum().toFixed(2) }}</p>
        </div>
      </div>
      <button class="continue-btn" @click="sendSelectedDishes()">Continue to Payment</button>
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
  padding-bottom: 24px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
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

.headings {
  padding-bottom: 24px;
}

.heading__qty-price {
  gap: 43px;
}

.selector-line {
  height: 0.5px;
  background-color: var(--base-dark-line);
  opacity: 0.5;
  width: 100%;
  display: flex;


}

.loading {

  color: var(--white);
  font-family: 'Barlow';
  font-size: 20px;
  font-style: normal;
  font-weight: 600;
  line-height: 140%;
}

.selected-dishes {
  max-height: 455px;
  height: 100%;
  padding-top: 24px;
  flex-wrap: wrap;
  justify-content: space-between;
  overflow-y: none;
  overflow-x: hidden;
}

.selected-dishes::-webkit-scrollbar {
  display: none;

}

.selected-dishes-empty {
  display: flex;
  flex-direction: column;
  height: 100%;
  align-items: center;
  justify-content: center;
}

.total {
  margin-top: 24px;
  max-height: 62px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
  margin-bottom: 42px;
  gap: 20px;
}

.total div {
  display: flex;
  justify-content: space-between;
}

.total__title {

  font-family: 'Barlow';
  font-weight: 400;
  font-size: 14px;
  line-height: 140%;
  color: var(--text-light);
}

.total__value {
  font-family: 'Barlow';
  font-weight: 500;
  font-size: 16px;
  line-height: 140%;
  color: var(--white);
}

.continue-btn {
  width: 100%;
  min-height: 48px;
  background: var(--primary-color);
  color: var(--base);

  border-radius: 8px;
  border: 1px;
  border-color: yellow;
  margin-top: auto;
  font-family: 'Barlow';
  font-style: normal;
  font-weight: 600;
  font-size: 14px;
  line-height: 140%;

}

.continue-btn:hover {
  box-shadow: 0px 8px 24px rgba(234, 124, 105, 0.3);
  cursor: pointer;

}
</style>