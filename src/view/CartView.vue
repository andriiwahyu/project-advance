<template>
  <div class="mb-5">
    <RouterLink to="/">
      <Button
        color="btn-outline-secondary"
        text="Go to home page"
      />
    </RouterLink>
  </div>
  <Cart 
    :data="availableCart" 
    :totalPrice="totalPriceCart"
    :totalItemCart="totalItemCart"
    @delete-item="deleteItem" 
    @delete-all="deleteAllItem"
    @checkout="checkout"
  />
</template>

<script setup>
import Cart from '../components/Cart.vue';
import Button from '../components/Button.vue';
import { RouterLink } from 'vue-router';
import { useStore } from 'vuex';
import { computed } from 'vue';
import Swal from 'sweetalert2'

const store = useStore();

const availableCart = computed(() => store.getters.availableCart);
const totalItemCart = computed(() => store.getters.totalItemCart);
const totalPriceCart = computed(() => store.getters.totalPriceCart);

const deleteItem = (id) => {
  store.commit('deleteOneItemCart',id)
}

const deleteAllItem = (id) => {
  store.commit('deleteAllItemCart',id)
}

const checkout = () => {
  Swal.fire(
    'Want to checkout?',
    `Total Price: ${totalPriceCart.value}`,
    'question'
  ).then((result) => {
    if (result.isConfirmed) {
      Swal.fire(
        'Checkout Success!',
        'Thank you for shopping with us',
        'success'
      ).then(() => {
        location.reload()
      })
    }
  })
}

</script>