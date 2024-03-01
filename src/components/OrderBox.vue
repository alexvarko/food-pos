<script setup>
import { ref, onMounted, onBeforeUnmount, watch, computed, watchEffect } from 'vue'
import SelectedDish from './SelectedDish.vue'
import PaymentForm from './PaymentForm.vue'
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


const paymentEnable = ref(false)
const container = ref(null)
const containerOffsetWidth = ref('')

const updateContainerWidth = () => {
  if (paymentEnable) {
    containerOffsetWidth.value = container.value.offsetWidth + 'px'
  }
}

onMounted(() => {
  // Initialize child width on mount
  updateContainerWidth()

  // Listen for window resize events and update child width accordingly
  window.addEventListener('resize', updateContainerWidth)
})

onBeforeUnmount(() => {
  // Clean up resize event listener
  window.removeEventListener('resize', updateContainerWidth)
})

const stepToPayment = () => {
  paymentEnable.value = !paymentEnable.value
}


</script>


<template>
  <div class="container" ref="container" @resize="updateContainerWidth">
    <div class="container__inner" :class="[paymentEnable ? 'confirment-shift' : '']">

      <div v-if="!paymentEnable">
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
      </div>

      <div v-else>
        <div class="return-arrow">
          <svg @click="paymentEnable = !paymentEnable" width="24" height="24" viewBox="0 0 24 24" fill="none"
            xmlns="http://www.w3.org/2000/svg">
            <path d="M8.5 16.5L4 12M4 12L8.5 7.5M4 12L20 12" stroke="white" stroke-width="1.8" stroke-linecap="round"
              stroke-linejoin="round" />
          </svg>
        </div>
        <div class="confirment__heading">
          <div class="titles">
            <h1 class="heading-title">Confirmation</h1>
            <p class="heading-subtitle">Orders #{{ randomnumber }}</p>
          </div>
          <div class="confirment__heading-add-btn">
            <div class="sidebar__menu-image-box">

              <svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M9 1.5V9M9 16.5V9M9 9H16.5M9 9H1.5" stroke="#FAFAFA" stroke-width="1.8" stroke-linecap="round"
                  stroke-linejoin="round" />
              </svg>

            </div>
          </div>
        </div>

      </div>
      <div class="selector-line"></div>
      <div class="selected-dishes" :style="[!paymentEnable ? 'padding-top: 24px;' : '']">
        <h3 v-if="!dishesSelectedList.length" class="loading selected-dishes-empty">Select Dish to order</h3>
        <SelectedDish v-else v-for="dish in dishesSelectedList" :selectedDish="dish" :key="dish.id"
          :originalList="dishesSelectedList"></SelectedDish>
      </div>
      <div class="selector-line"></div>
      <div class="total" :style="[!paymentEnable ? 'margin-top: 24px' : '']">
        <div class="discount">
          <p class="total__title">Discount</p>
          <p class="total__value">$0</p>
        </div>
        <div class="sum">
          <p class="total__title">Sub total</p>
          <p class="total__value">$ {{ totalSum().toFixed(2) }}</p>
        </div>
      </div>
      <button v-if="!paymentEnable" class="continue-btn" @click="stepToPayment()">Continue to Payment</button>

    </div>
    <div class="container__inner" :class="[paymentEnable ? 'payment-shift' : 'payment-hidden']">
      <div class="payment__heading">
        <div class="titles">
          <h1 class="heading-title">Payment</h1>
          <p class="heading-subtitle">3 payment methods available</p>
        </div>
      </div>
      <div class="selector-line"></div>
      <PaymentForm :orderType="orderTypeFromDishes"></PaymentForm>
      <div class="payment-btns">
            <button class="cancel-btn" @click="sendSelectedDishes()">Cancel</button>
            <button class="continue-btn" @click="stepToPayment()">Confirm Payment</button>
        </div>
    </div>
  </div>
</template>



<style lang="scss" scoped>
.container {
  height: 100%;
  width: 100%;
  position: relative;
  display: flex;

}

.container__inner {
  background-color: var(--base-dark-bg-2);
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
  position: absolute;
  padding-left: 24px;
  padding-top: 24px;
  padding-right: 24px;
  padding-bottom: 24px;
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  z-index: 999;
}

.confirment-shift {
  right: v-bind(containerOffsetWidth);
  border-top-left-radius: 16px;
  border-bottom-left-radius: 16px;
  border-right: 1px solid var(--base-dark-line);
}

.payment-hidden {
  right: -1000px;
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
  margin-top: auto;
  font-family: 'Barlow';
  font-style: normal;
  font-weight: 600;
  font-size: 14px;
  line-height: 140%;

}

.cancel-btn {
  width: 100%;
  min-height: 48px;
  background: transparent;
  color: var(--primary-color);

  border-radius: 8px;
  border: 1px solid ;
  margin-top: auto;
  font-family: 'Barlow';
  font-style: normal;
  font-weight: 600;
  font-size: 14px;
  line-height: 140%;
  cursor: pointer;
}

.continue-btn:hover {
  box-shadow: 0px 8px 24px rgba(234, 124, 105, 0.3);
  cursor: pointer;

}

.return-arrow {
  padding-bottom: 16px;

  svg {
    cursor: pointer;
  }
}

.confirment__heading {
  display: flex;
  justify-content: space-between;
}

.payment__heading {
  margin-top: 40px;
  margin-bottom: 24px;
}

.heading-title {
  font-family: 'Barlow';
  font-weight: 600;
  font-size: 28px;
  line-height: 140%;
  color: var(--white);
  margin-bottom: 8px;
}

.heading-subtitle {
  font-family: 'Barlow';
  font-weight: 500;
  font-size: 16px;
  line-height: 140%;
  color: var(--text-light);
}

.confirment__heading-add-btn {
  margin-top: 9px;
  border-radius: 8px;
  background: var(--primary-color);
  width: 48px;
  height: 48px;
  flex-shrink: 0;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.confirment__heading-add-btn:hover {
  box-shadow: 0px 8px 24px rgba(234, 124, 105, 0.3);

}



.input-field {

  width: 100%;
  height: 48px;

  background: var(--base-form-bg);
  border: 1px solid var(--base-dark-line);
  border-radius: 8px;
  margin-bottom: 16px;
  padding-left: 14px;
  color: var(--text-lighter);
}

.input-label {
  margin-bottom: 8px;
  font-family: 'Barlow';
  font-style: normal;
  font-weight: 500;
  font-size: 14px;
  line-height: 130%;
  color: var(--white);
}

.two-input-in-row {
  display: flex;
  justify-content: space-between;
  gap: 13px;
}

.payment-btns{
  display: flex;
  gap: 6px;
}
</style>