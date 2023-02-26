<template>
  <Products 
    :data="availableProducts" 
    @add-item="addOneItem" 
    @add-all="addAllItem"
  />
  <div class="mt-5">
    <RouterLink to="/cart">
      <Button
        color="btn-outline-secondary"
        text="Go to cart page"
      />
    </RouterLink>
  </div>
</template>

<script setup>
import Products from '../components/Products.vue';
import Button from '../components/Button.vue';
import { useStore } from 'vuex';
import { computed } from 'vue';
import { RouterLink } from 'vue-router';

const store = useStore();

const availableProducts = computed(() => store.getters.availableProducts);

const addOneItem = (id) => {
  store.commit('addOneItem',id)
}

const addAllItem = (id) => {
  store.commit('addAllItem',id)
}

</script>

