<template>
    <div class="container mx-auto p-4">
        <h1 class="text-3xl font-semibold mb-4">Shopping Cart</h1>
        <table class="min-w-full divide-y divide-gray-200">
            <thead>
                <tr>
                    <th
                        class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
                        Item</th>
                    <th
                        class="px-6 py-3 bg-gray-50 text-right text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
                        Quantity</th>
                    <th
                        class="px-6 py-3 bg-gray-50 text-right text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
                        Price</th>
                    <th
                        class="px-6 py-3 bg-gray-50 text-right text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
                        Total</th>
                    <th class="px-6 py-3 bg-gray-50"></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, index) in cart" :key="item.id">
                    <td class="px-6 py-4 whitespace-no-wrap">
                        {{ item.name }}
                    </td>
                    <td class="px-6 py-4 text-right">
                        <select v-model="item.quantity" @change="updateCart(item, index)"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
                            <option selected>1</option>
                            <option value="2">2</option>
                            <option value="3">3</option>
                            <option value="4">4</option>
                            <option value="5">5</option>
                            <option value="6">6</option>
                            <option value="7">7</option>
                            <option value="8">8</option>
                            <option value="9">9</option>
                            <option value="10">10</option>
                        </select>
                    </td>
                    <td class="px-6 py-4 text-right">
                        {{ item.price }} L.E
                    </td>
                    <td class="px-6 py-4 text-right">
                        {{ item.price * item.quantity }} L.E
                    </td>
                    <td class="px-6 py-4 text-right">
                        <button @click="removeFromCart(index)" class="text-red-600 hover:text-red-800">Remove</button>
                    </td>
                </tr>
            </tbody>
        </table>

        <div class="mt-4">
            <p class="text-right font-semibold">Total: {{ cartTotal }} L.E</p>
        </div>

        <div class="mt-6 text-right">
            <div>
                <RouterLink to="/payment" class="ml-4 bg-indigo-500 text-white px-4 py-2 rounded-md hover:bg-indigo-600">
                    Proceed to
                    Payment</RouterLink>
            </div>
            <div class="mt-6 justify-end text-sm text-gray-500">
                <p>Or
                    <RouterLink to="/" class="font-medium text-indigo-600 hover:text-indigo-500">
                        Continue Shopping
                        <span aria-hidden="true"> &rarr;</span>
                    </RouterLink>
                </p>
            </div>
        </div>
    </div>
</template>
  
<script setup>
import { computed, onMounted } from 'vue';
import { useCart } from '../shared/Cart.vue';

const { cart, getCart, updateCart, removeFromCart } = useCart();
let cartTotal = computed(() => cart.value.reduce((total, item) => total + item.price * item.quantity, 0))

onMounted(() => {
  getCart();
})

</script>