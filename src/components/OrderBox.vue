<script setup>
import { ref, onMounted } from 'vue'

function getRandomInt(max) {
  return Math.floor(Math.random() * max);
}



const randomnumber = ref(null)
onMounted(() => {
  randomnumber.value = getRandomInt(1000)

})

</script>


<template>
  <div class="container">
    <div class="container__inner">
      <div class="order__id">
        <h2 class="order__id-title">Orders #{{ randomnumber }}</h2>
      </div>
      <div class="order__type">
        <div class="order__type-btn order__type-btn--active">
          <p class="type-btn__name">
            Dine In
          </p>
        </div>
        <div class="order__type-btn">
          <p class="type-btn__name">
            To Go
          </p>
        </div>
        <div class="order__type-btn">
          <p class="type-btn__name">
            Delivery
          </p>
        </div>
      </div>
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
}

.order__type-btn {
  min-width: 54px;
  height: 34px;
  border: 1px solid var(--base-dark-line);
  border-radius: 8px;

}

.type-btn__name {
  display: flex;
  padding: 7px 12px;
  justify-content: center;
  align-items: center;
  color: var(--white);
  font-family: "Barlow";
  font-size: 14px;
  font-style: normal;
  font-weight: 600;
  line-height: 140%;

}

.order__type-btn--active {
  background-color: var(--primary-color);
  border: none;
}
</style>