<script setup lang="ts">
import type { ProductInterface } from '@/interfaces/Product.interface'
import CartProductList from './CartProductList.vue'

defineProps<{
  cart: ProductInterface[]
}>()

const emit = defineEmits<{
  (e: 'removeProductFromCart', productId: number): void
}>()
</script>

<template>
  <div class="container">
    <h2 class="title">Panier</h2>
    <cart-product-list
      :cart="cart"
      @remove-product-from-cart="emit('removeProductFromCart', $event)"
    />
  </div>
</template>

<style scoped lang="scss ">

.container {
  padding: 20px;
}
</style>
@/interfaces/Product.interface
