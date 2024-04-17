<script setup>
import { ref, onMounted, defineEmits } from 'vue'
import ManageDishCard from './ManageDishCard.vue';
const dishes = ref(null)
const dishesContainer = ref(null);

const calculateMaxHeight = () => {
    if (dishesContainer.value) {
        const windowHeight = window.innerHeight;
        const containerTopOffset = dishesContainer.value.getBoundingClientRect().top;
        const calculatedMaxHeight = windowHeight - containerTopOffset - /* Add additional offset if needed */ 16;
        dishesContainer.value.style.maxHeight = `${calculatedMaxHeight + 20}px`;
    }
};
onMounted(() => {
    setTimeout(() => {
        fetch('http://localhost:3001/dishes')
            .then(response => response.json())
            .then(data => dishes.value = data)
    }, 2000);
    calculateMaxHeight(); // Calculate initially
    window.addEventListener('resize', calculateMaxHeight);

})

const props = defineProps(['orderType', 'selectedDishes']);
const emits = defineEmits();

const selected = ref("dineIn");
const dishesSelectedList = ref([])

const emitSelected = () => {
    emits('update:orderType', selected.value);
};

const addDish = (dish) => {
    const index = dishesSelectedList.value.findIndex(item => item.id === dish.id);

    if (index !== -1) {
        dishesSelectedList.value[index].amount++;
    } else {
        dishesSelectedList.value.push({ ...dish, amount: 1, description: "" });
    }

    emits('update:selectedDishes', dishesSelectedList.value);
}

</script>

<template>
    <div class="dishes-container" ref="dishesContainer">
        <h3 v-if="!dishes" class="loading">Loading....</h3>
        <div class="new-item" v-if="dishes">
            <div class="add-btn">
                <svg width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M9 1.5V9M9 16.5V9M9 9H16.5M9 9H1.5" stroke="#EA7C69" stroke-width="1.8"
                        stroke-linecap="round" stroke-linejoin="round" />
                </svg>

                <p class="add-title">Add new dish</p>
            </div>
        </div>
        <ManageDishCard v-if="dishes" v-for="dishitem in dishes.data" :dish="dishitem" :key="dishitem.id">{{ dish }}
        </ManageDishCard>
    </div>
    <div class="buttons">
        <div class="discard-btn"><span>Discard Changes</span></div>
        <div class="save-btn"><span>Save Changes</span></div>
    </div>
</template>

<style lang="scss" scoped>
.buttons {
    gap: 8px;
    display: flex;
    position: absolute;
    bottom: 0;
    margin-left: 24px;
    margin-bottom: 24px;

    div {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        padding: 14px;
        gap: 8px;
        min-width: 172px;
        height: 48px;
        border-radius: 8px;
        font-family: 'Barlow';
        font-style: normal;
        font-weight: 600;
        font-size: 14px;
        line-height: 140%;
    }
}

.discard-btn {

    border: 1px solid var(--primary-color);

    color: var(--primary-color);

}

.discard-btn:hover{
    cursor: pointer;
    border-color: rgb(255, 124, 163);
    color: rgb(255, 124, 163);
}

.save-btn {
    background: var(--primary-color);
    color: var(--white);
}

.save-btn:hover{
    cursor: pointer;
    box-shadow: 0px 8px 24px rgba(234, 124, 105, 0.4);
}
.new-item {
    min-height: 299px;
    width: 221px;
    position: relative;
    display: flex;
    flex-direction: column;
    margin-bottom: 24px;
    padding-top: 24px;
    border: 1px dashed var(--primary-color);
    border-radius: 8px;
    align-items: center;
    justify-content: center;
    transition: all .3s ease;
}

.new-item:hover{
    border-color: rgb(255, 124, 163);
    cursor: pointer;
    .add-btn{
    color: rgb(255, 124, 163);

    svg {
        path {
            stroke: rgb(255, 124, 163);
        }
    }
}
}

.add-btn {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    font-family: 'Barlow';
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 140%;
    color: var(--primary-color);
}



.dishes-container {
    gap: 10px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    overflow-y: auto;
    overflow-x: hidden;
    margin: 0 24px;
    height: 60%;
    position: absolute;

}

.dishes-container::-webkit-scrollbar {
    display: none;
}


.loading {

    color: var(--white);
    font-family: 'Barlow';
    font-size: 20px;
    font-style: normal;
    font-weight: 600;
    line-height: 140%;
}
</style>