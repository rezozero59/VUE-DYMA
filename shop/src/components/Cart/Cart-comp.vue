<script setup lang="ts">
import type { ProductCartInterface } from '@/interfaces'
import CartProductList from './CartProductList.vue'

defineProps<{
  cart: ProductCartInterface[]
}>()

const emit = defineEmits<{
  (e: 'removeProductFromCart', productId: number): void
}>()
</script>

<template>
  <div class="container d-flex flex-column">
    <h2 class="title">Panier</h2>
    <cart-product-list
      class="flex-fill"
      :cart="cart"
      @remove-product-from-cart="emit('removeProductFromCart', $event)"
    />
    <button class="btn btn-success">Commander ()</button>
  </div>
</template>

<style scoped lang="scss ">

.container {
  padding: 20px;
}
</style>
