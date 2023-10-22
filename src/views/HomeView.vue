<template>
  <div class="bg-white">
    <div class="mx-auto max-w-2xl px-4 py-16 sm:px-6 sm:py-24 lg:max-w-7xl lg:px-8">
      <h2 class="sr-only">Products</h2>

      <div class="grid grid-cols-1 gap-x-6 gap-y-10 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 xl:gap-x-8">
        <!-- Item Listing -->
        <span v-for="item in items.data" :key="item.id" :href="item.href" class="group">
          <div
            class="container aspect-h-1 aspect-w-1 w-full overflow-hidden rounded-lg bg-gray-200 xl:aspect-h-8 xl:aspect-w-7">
            <img src="@/assets/noimg.jpg" alt="No image"
              class="h-full w-full object-cover object-center group-hover:opacity-75" />
            <div class="overlay px-2 mx-2">
              <p>{{ item.description }}</p>
            </div>
          </div>
          <h3 class="mt-4 text-sm text-gray-700">{{ item.name }}</h3>
          <p class="mt-1 text-lg font-medium text-gray-900">{{ item.price }}</p>
          <div class="mx-1 my-2 flex justify-between">

            <select v-model="item.quantity"
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

            <button @click="addToCart(item)"
              class="bg-cyan-400 hover:bg-cyan-500 text-white font-bold py-2 px-4 rounded inline-flex items-center">
              <svg class="flex-1 w-8 h-8 fill-current" viewbox="0 0 24 24">
                <path
                  d="M17,18C15.89,18 15,18.89 15,20A2,2 0 0,0 17,22A2,2 0 0,0 19,20C19,18.89 18.1,18 17,18M1,2V4H3L6.6,11.59L5.24,14.04C5.09,14.32 5,14.65 5,15A2,2 0 0,0 7,17H19V15H7.42A0.25,0.25 0 0,1 7.17,14.75C7.17,14.7 7.18,14.66 7.2,14.63L8.1,13H15.55C16.3,13 16.96,12.58 17.3,11.97L20.88,5.5C20.95,5.34 21,5.17 21,5A1,1 0 0,0 20,4H5.21L4.27,2M7,18C5.89,18 5,18.89 5,20A2,2 0 0,0 7,22A2,2 0 0,0 9,20C9,18.89 8.1,18 7,18Z" />
              </svg> <span>Add To Cart</span>
            </button>
          </div>
        </span>
        <!-- End of Product Listing -->

        <!-- Pagination -->
        <TailwindPagination :data="items" @pagination-change-page="fetchItems" />
        <!-- End of Pagination -->
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios';
import { TailwindPagination } from 'laravel-vue-pagination';
import { useCart } from '../shared/Cart.vue';

const { addToCart, getCart } = useCart();

let items = ref([])

const fetchItems = async (page = 1) => {
  try {
    const response = await axios.get('/items?page=' + page, {
      'Content-Type': 'application/json'
    });
    items.value = response.data;
  } catch (error) {
    console.error('Error fetching items:', error);
  }
};

onMounted(() => {
  fetchItems();
  getCart();
})

</script>

<style scoped>
input {
  width: 50px;
}

.container {
  position: relative;
  /* width: 300px; */
}

.image {
  width: 100%;
  height: auto;
  display: block;
}

.overlay {

  position: absolute;
  max-height: 48px;
  bottom: 0px;
  /* background-color: rgba(241, 237, 237, 0.7);
  color: rgba(241, 237, 237, 0.7); */
  background-color:  rgba(241, 237, 237, 0.7);
  color: #333;
  transition: bottom 0.5s;
}

.overlay:hover {
  background-color:  rgba(241, 237, 237, 0.7);
  color: #333;
}
</style>