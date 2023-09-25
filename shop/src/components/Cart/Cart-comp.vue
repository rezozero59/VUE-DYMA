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
