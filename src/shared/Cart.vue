<script>

import { ref } from 'vue';
import axios from 'axios';

export const cart = ref([]);
export const storeCredit = ref(0);

export function useCart() {

  const addToCart = async (item) => {
    if (!item.quantity) {
      item.quantity = 1;
    }

    try {

      const response = await axios.post('/cart/1', {
        item_id: item.id,
        quantity: item.quantity
      });

      if (response.data.id) {
        getCart();
      }

    } catch (error) {
      alert(error.response.data.message);
      console.error('Error adding an item:', error);
    }
  };

  const updateCart = async (item, index) => {
    if (!item.quantity) {
      item.quantity = 1;
    }

    try {
      const response = await axios.put('/cart/' + item.id, {
        item_id: item.id,
        quantity: item.quantity
      });

      cart.value[index].quantity = parseInt(item.quantity);

    } catch (error) {
      console.error('Error fetching products:', error);
    }
  };

  const getCart = async () => {
    try {
      const response = await axios.get('/cart/1', {
        'Content-Type': 'application/json'
      });

      cart.value = response.data.data;
      storeCredit.value = response.data.store_credit;
    } catch (error) {
      console.error('Error fetching items:', error);
    }
  };

  const removeFromCart = async (index) => {

    try {
      const response = await axios.delete('/cart/' + cart.value[index].id, {
        'Content-Type': 'application/json'
      });

      cart.value.splice(index, 1);
    } catch (error) {
      console.error('Error fetching items:', error);
    }
  };

  const removeAllCart = () => {
    cart.value.splice(0, cart.value.length);
  }

  const getCartCount = () => {
    return cart.value.reduce((total, item) => total + parseInt(item.quantity), 0);
  }

  // getCart()

  return {
    cart,
    storeCredit,
    getCartCount,
    getCart,
    addToCart,
    updateCart,
    removeFromCart,
    removeAllCart
  };
}

</script>

