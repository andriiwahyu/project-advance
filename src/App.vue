<template>
  <Nav @add-product="addProduct" @show-add-form="showAddForm" />
  <main class="py-3 px-5">
    <AddForm
      v-if="addForm"
      v-model:name="addFormData.name"
      v-model:description="addFormData.description"
      v-model:price="addFormData.price"
      v-model:stock="addFormData.stock"
      @add-product="addProduct"
      @show-add-form="showAddForm"
  />
    <RouterView />
  </main>
</template>

<script setup>
import Nav from './components/Nav.vue'
import AddForm from './components/AddForm.vue';
import { ref,reactive } from 'vue';
import { RouterView } from 'vue-router';
import { useStore } from 'vuex'

const store = useStore()

const addForm = ref(false)
const showAddForm = () => {
  addForm.value = !addForm.value
}

const addFormData = reactive({
  id: Math.floor(Math.random() * 500),
  name: '',
  description: '',
  stock: 0,
  price: 0
})

const addProduct = () => {
  store.commit('addProduct',addFormData)
  addForm.value = false
}

</script>
