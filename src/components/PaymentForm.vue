<script setup>
import { ref } from 'vue'
const paymentMethod = ref('card')
const cardholderName = ref('')
const cardNumber = ref('')
const expirationDate = ref('')
const cvvCode = ref('')
const props = defineProps(['orderType'])
const orderTypeName = { 'dineIn': 'Dine In', 'toGo': 'To Go', 'delivery': 'Delivery' }

</script>

<template>
    <div class="payment__form">
        <h2 class="payment__form-title">Payment Method</h2>
        <div class="payment__form-methods">
            <label class="pay-method-label" for="card">
                <input type="radio" id="card" name="pay-method" value="card" class="pay-method-input" checked
                    v-model="paymentMethod" />
                <svg width="23" height="16" viewBox="0 0 23 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path fill-rule="evenodd" clip-rule="evenodd"
                        d="M0.75 5C0.75 2.37665 2.87665 0.25 5.5 0.25H17.5C20.1234 0.25 22.25 2.37665 22.25 5V11C22.25 13.6234 20.1234 15.75 17.5 15.75H5.5C2.87665 15.75 0.75 13.6234 0.75 11V5ZM2.33697 4.25H20.663C20.3245 2.81665 19.0368 1.75 17.5 1.75H5.5C3.96321 1.75 2.67555 2.81665 2.33697 4.25ZM20.75 5.75H2.25V11C2.25 12.7949 3.70507 14.25 5.5 14.25H17.5C19.2949 14.25 20.75 12.7949 20.75 11V5.75ZM12.75 11C12.75 10.5858 13.0858 10.25 13.5 10.25H17.5C17.9142 10.25 18.25 10.5858 18.25 11C18.25 11.4142 17.9142 11.75 17.5 11.75H13.5C13.0858 11.75 12.75 11.4142 12.75 11Z"
                        fill="#ABBBC2" />
                </svg>
                <span>Credit Card</span>
            </label>
            <label class="pay-method-label" for="paypal">
                <input type="radio" id="paypal" name="pay-method" value="paypal" class="pay-method-input"
                    v-model="paymentMethod" />
                <svg width="20" height="20" viewBox="0 0 7.5 7.5" xmlns="http://www.w3.org/2000/svg" fill="red"
                    stroke="red">
                    <g stroke-width="0" />
                    <g stroke-linecap="round" stroke-linejoin="round" />
                    <g stroke="none" fill="none" fill-rule="evenodd">
                        <path
                            d="M3.919.625c.877 0 1.575.628 1.732 1.421.587.301.949.962.827 1.658l-.014.072-.015.068a1.875 1.875 0 0 1-1.753 1.467l-.077.002h-.454l-.162 1.034a.625.625 0 0 1-.567.526l-.051.002h-.617a.625.625 0 0 1-.623-.579l-.002-.046h-.528a.625.625 0 0 1-.623-.676l.005-.045.643-4.111a.94.94 0 0 1 .871-.791l.055-.002zm1.715 2.183-.003.011a2.056 2.056 0 0 1-1.993 1.556H3.06l-.244 1.563h.001l-.049.313h.617l.162-1.034a.625.625 0 0 1 .618-.529h.454a1.25 1.25 0 0 0 1.22-.979l.015-.068a.93.93 0 0 0-.22-.833M3.919 1.25H2.566a.31.31 0 0 0-.301.23l-.007.034-.643 4.111h.617l.21-1.347a.625.625 0 0 1 .567-.526l.051-.002h.577c.656 0 1.228-.446 1.388-1.082a1.14 1.14 0 0 0-1.047-1.416z"
                            fill="#ABBBC2" />
                    </g>
                </svg>
                <span>Paypal</span>
            </label>
            <label class="pay-method-label" for="cash">
                <input type="radio" id="cash" name="pay-method" value="cash" class="pay-method-input"
                    v-model="paymentMethod" />
                <svg width="21" height="20" viewBox="0 0 21 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M14.688 0.5C17.8978 0.5 20.5 3.16116 20.5 6.44374V13.5563C20.5 16.8388 17.8978 19.5 14.688 19.5H6.31204C3.10219 19.5 0.5 16.8388 0.5 13.5563V6.44374C0.5 3.16116 3.10219 0.5 6.31204 0.5H14.688ZM14.688 1.98651H6.31204C3.90498 1.98651 1.95358 3.98213 1.95358 6.44374V13.5563C1.95358 16.0179 3.90498 18.0135 6.31204 18.0135H14.688C17.095 18.0135 19.0464 16.0179 19.0464 13.5563L19.046 13.279L15.8499 13.2798C14.0084 13.2787 12.5159 11.7531 12.5147 9.86949C12.5147 8.04914 13.9101 6.56244 15.6673 6.46431L15.8504 6.45916L19.046 6.459L19.0464 6.44374C19.0464 4.05454 17.2081 2.10431 14.8991 1.99165L14.688 1.98651ZM19.046 7.945L15.8508 7.94567C14.8109 7.94632 13.9683 8.80743 13.9683 9.86904C13.9689 10.8811 14.7329 11.7102 15.7033 11.7874L15.8504 11.7933L19.046 11.793V7.945ZM16.2942 9.06518C16.6956 9.06518 17.021 9.39795 17.021 9.80844C17.021 10.1847 16.7475 10.4957 16.3928 10.5449L16.2942 10.5517H15.9921C15.5907 10.5517 15.2653 10.2189 15.2653 9.80844C15.2653 9.43215 15.5388 9.12118 15.8935 9.07196L15.9921 9.06518H16.2942ZM10.8539 4.99736C11.2553 4.99736 11.5807 5.33013 11.5807 5.74062C11.5807 6.1169 11.3073 6.42788 10.9525 6.47709L10.8539 6.48388H5.62203C5.22063 6.48388 4.89524 6.15111 4.89524 5.74062C4.89524 5.36434 5.16866 5.05337 5.5234 5.00415L5.62203 4.99736H10.8539Z"
                        fill="#ABBBC2" />
                </svg>
                <span>Cash</span>
            </label>
        </div>
        <p class="input-label">Cardholder Name</p>
        <input type="text" id="name" name="name" class="input-field" placeholder="Levi Ackerman" v-model="cardholderName" />
        <p class="input-label">Card Number</p>
        <input type="text" id="card-number" name="name" class="input-field" placeholder="2564 1421 0897 1244"
            v-model="cardNumber" />
        <div class="two-input-in-row">
            <div>
                <p class="input-label">Expiration Date</p>
                <input type="text" id="expiration-date" name="name" class="input-field" placeholder="02/2024"
                    v-model="expirationDate" />
            </div>
            <div>
                <p class="input-label">CVV</p>
                <input type="password" id="cvv-code" name="name" class="input-field" placeholder="123" v-model="cvvCode" />
            </div>

        </div>
        <div class="selector-line" style="margin-top: 24px;"></div>
        <div class="two-input-in-row">
            <div>
                <p class="input-label">Order Type</p>
                <input class="selection" :placeholder="orderTypeName[orderType]" disabled />
            </div>
            <div>
                <p class="input-label">Table no.</p>
                <input type="text" id="table-number" name="name" class="input-field"
                    :placeholder="Math.floor(Math.random() * 200)" disabled />
            </div>
        </div>
       
    </div>
</template>


<style lang="scss" scoped>

.selector-line {
  height: 0.5px;
  background-color: var(--base-dark-line);
  opacity: 0.5;
  width: 100%;
  display: flex;
  margin-bottom: 24px;


}
.payment__form {
    margin-top: 24px;
    height: 100%;
}

.payment__form-title {
    font-family: 'Barlow';
    font-weight: 600;
    font-size: 20px;
    line-height: 140%;
    color: var(--white);
    margin-bottom: 16px;
}

.pay-method-input {
    visibility: hidden;
    height: 0px;
}

.payment__form-methods {
    display: flex;
    max-height: 64px;
    height: 100%;
    gap: 8px;
    margin-bottom: 16px;
}

.pay-method-label {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100px;
    justify-content: center;
    cursor: pointer;

    svg {
        margin-bottom: 6px;
    }

    font-family: 'Barlow';
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 130%;
    color: var(--text-light);
    border: 1px solid var(--base-dark-line);
    border-radius: 8px;


}

.pay-method-label:has(input:checked) {
    background: var(--base-dark-bg-1);
    border: 1px solid var(--text-light);
}

.pay-method-label:hover {
    background: var(--base-dark-bg-1);
    border: 1px solid var(--text-light);
}

.pay-method-input:checked+svg {
    path {
        fill: var(--white);
    }
}

.pay-method-input:checked~span {
    color: var(--white);
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


.input-field::placeholder {

    font-family: 'Barlow';
    font-weight: 400;
    font-size: 14px;
    line-height: 140%;

    color: var(--text-lighter);
}

.input-field[type="password"] {
    font: small-caption;
    font-size: 27px
}

.two-input-in-row {
    display: flex;
    justify-content: space-between;
    gap: 13px;
}
.selection {
  display: inline-flex;
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
  width: 100%;
  padding-left: 44px;
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

.selection[disabled]::placeholder {
  color: var(--white);
}

input[disabled] {
  opacity: 1;
}
</style>