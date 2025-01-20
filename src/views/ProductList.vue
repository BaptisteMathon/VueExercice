<script lang="ts">
import {ref} from 'vue'
export default {
  name: 'ProductList',
  setup(){
    const ListProducts = ref([
      {id: 1, label: 'Carotte', description: "de belles carottes", statut: "disponible", quantity: 5},
      {id: 2, label: 'Pomme de terre', description: "de belles pomme de terre", statut: "disponible", quantity: 0},
      {id: 3, label: 'Pomme', description: "de belle pomme", statut: "disponible", quantity: 15},
    ])

    ListProducts.value.forEach(element => {
      element.statut = element.quantity === 0 ? "indisponible" : "disponible"
    });

    return {
      ListProducts,

    }
  }
}
</script>

<template>
  <div>
    <h1>Product List</h1>
    <ul>
      <li v-for="product in ListProducts">
        {{ product.label }} : {{ product.description }} ( {{ product.statut }} )
      </li>
    </ul>
  </div>
</template>
