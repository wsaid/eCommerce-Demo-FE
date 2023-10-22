<template>
    <div>
        <h1 class="text-2xl font-bold mb-4">Payment Page</h1>
        <form @submit.prevent="placeOrder" class="max-w-md mx-auto">
            <div class="mb-4">
                <label for="address" class="block text-sm font-medium text-gray-700">Address:</label>
                <input v-model="address" id="address" name="address" type="text" required
                    class="mt-1 p-2 w-full border border-gray-300 rounded focus:ring focus:ring-indigo-200" />
                <span class="text-red-500" v-if="formErrors.address">{{ formErrors.address[0] }}</span>

            </div>

            <div class="mb-4">
                <label for="telephone" class="block text-sm font-medium text-gray-700">Telephone:</label>
                <input v-model="phone" id="phone" name="phone" type="text" required
                    class="mt-1 p-2 w-full border border-gray-300 rounded focus:ring focus:ring-indigo-200" />
                <span class="text-red-500" v-if="formErrors.phone">{{ formErrors.phone[0] }}</span>

            </div>
            <span class="text-red-500" v-if="formErrors.order_total">{{ formErrors.order_total[0] }}</span>

            <div class="flex justify-between">
                <RouterLink to="/cart"
                    class="px-4 py-2 text-sm font-medium text-gray-600 bg-gray-200 rounded hover:bg-gray-300 focus:outline-none focus:ring focus:ring-gray-300">
                    Cancel</RouterLink>

                <button type="submit"
                    class="px-4 py-2 text-sm font-medium text-white bg-indigo-500 rounded hover:bg-indigo-600 focus:outline-none focus:ring focus:ring-indigo-300">
                    Place Order
                </button>
            </div>
        </form>
    </div>
</template>
  
<script>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import axios from 'axios';
import { storeCredit, useCart } from '../shared/Cart.vue';

const { removeAllCart } = useCart();

export default {
    setup() {
        const address = ref('');
        const phone = ref('');
        const router = useRouter();
        const formErrors = ref({});

        const placeOrder = async () => {

            formErrors.value = {};

            try {
                const response = await axios.post('/place-order/1', {
                    address: address.value,
                    phone: phone.value,
                    order_total: 100

                });

                if (response.status === 201) {
                    removeAllCart();

                    if (response.data.storeCredit) {
                        storeCredit.value = response.data.store_credit;
                    }
                    router.push('/payment-success');
                } else {
                    router.push('/payment-fail');

                }
            } catch (error) {
                if (error.response && error.response.status === 422) {
                    formErrors.value = error.response.data.errors;
                } else {
                    console.log(error)
                }
            }
        };

        return { address, phone, formErrors, placeOrder };
    },
};
</script>