<template>
  <div class="bg-white">

    <header class="relative bg-white">
      <nav aria-label="Top" class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
        <div class="border-b border-gray-200">
          <div class="flex h-16 items-center">

            <!-- Logo -->
            <div class="ml-4 flex lg:ml-0">
              <a href="#">
                <img class="h-8 w-auto" src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=600" alt="" />
              </a>
            </div>

            <div class="ml-auto flex items-center">
              <div class="hidden lg:flex lg:flex-1 lg:items-center lg:justify-end lg:space-x-6">
                <slot name="links"></slot>
              </div>

              <div class="hidden lg:ml-8 lg:flex">
                <a href="#" class="flex items-center text-gray-700 hover:text-gray-800">

                  <IconWallet width="30px" height="30px" />
                  <span class="ml-3 block text-sm font-medium">{{ storeCredit }} EGP</span>
                </a>
              </div>

              <!-- Search -->
              <div class="flex lg:ml-6">
                <a href="#" class="p-2 text-gray-400 hover:text-gray-500">
                  <span class="sr-only">Search</span>
                </a>
              </div>

              <!-- Cart -->
              <li
                class="font-sans block mt-4 lg:inline-block lg:mt-0 lg:ml-6 align-middle text-black hover:text-gray-700">
                <slot name="cart"></slot>
                <RouterLink to="/cart" role="button" class="relative flex">
                  <svg class="flex-1 w-8 h-8 fill-current" viewbox="0 0 24 24">
                    <path
                      d="M17,18C15.89,18 15,18.89 15,20A2,2 0 0,0 17,22A2,2 0 0,0 19,20C19,18.89 18.1,18 17,18M1,2V4H3L6.6,11.59L5.24,14.04C5.09,14.32 5,14.65 5,15A2,2 0 0,0 7,17H19V15H7.42A0.25,0.25 0 0,1 7.17,14.75C7.17,14.7 7.18,14.66 7.2,14.63L8.1,13H15.55C16.3,13 16.96,12.58 17.3,11.97L20.88,5.5C20.95,5.34 21,5.17 21,5A1,1 0 0,0 20,4H5.21L4.27,2M7,18C5.89,18 5,18.89 5,20A2,2 0 0,0 7,22A2,2 0 0,0 9,20C9,18.89 8.1,18 7,18Z" />
                  </svg>
                  <span class="btn-circle">{{ getCartCount() }}
                  </span>
                </RouterLink>
              </li>
            </div>
          </div>
        </div>
      </nav>
    </header>
  </div>
</template>

<script setup>
  import IconWallet from './icons/IconWallet.vue';
  import { useCart } from '../shared/Cart.vue';

  const { storeCredit, getCartCount } = useCart();

  // const itemsCount = computed(() => cart.value.reduce((total, item) => total + parseInt(item.quantity), 0))

</script>

