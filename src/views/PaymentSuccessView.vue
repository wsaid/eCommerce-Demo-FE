<template>
    <main class="grid min-h-full place-items-center bg-white px-6 py-24 sm:py-32 lg:px-8">
      <div class="text-center">
        <p class="text-base font-semibold text-indigo-600">
            <svg class="h-8 w-8 text-green-500 inline"  width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round">  <path stroke="none" d="M0 0h24v24H0z"/>  <circle cx="12" cy="12" r="9" />  <line x1="9" y1="10" x2="9.01" y2="10" />  <line x1="15" y1="10" x2="15.01" y2="10" />  <path d="M9.5 15a3.5 3.5 0 0 0 5 0" /></svg>        </p>

        <h1 class="mt-4 text-3xl font-bold tracking-tight text-green-600 sm:text-5xl">Thank you for shopping with us!</h1>
        <p class="mt-6 text-base leading-7 text-gray-600">Thank you for being our valued customer. We hope our product will meet your expectations. Let us know if you have any questions.</p>
        <div class="mt-10 flex items-center justify-center gap-x-6">
            <RouterLink to="/" class="rounded-md bg-indigo-600 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
                Go back home
            </RouterLink>
          <a href="#" class="text-sm font-semibold text-gray-900">Track your order <span aria-hidden="true">&rarr;</span></a>
        </div>
      </div>
    </main>
  </template>

<script setup>
import { onMounted } from 'vue'
import { useCart } from '../shared/Cart.vue';

const { getCart } = useCart();



onMounted(() => {
  getCart();
})

</script>