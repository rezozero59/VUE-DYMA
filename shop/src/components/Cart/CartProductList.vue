<script setup lang="ts">
import type { ProductCartInterface } from '@/interfaces'
import CartProduct from './CartProduct.vue'
defineProps<{
  cart: ProductCartInterface[]
}>()

const emit = defineEmits<{
  (e: 'removeProductFromCart', productId: number): void
}>()
</script>

<template>
  <div class="product-container d-flex flex-column">
    <cart-product
      v-for="product of cart"
      :key="product.id"
      :product="product"
      @remove-product-from-cart="emit('removeProductFromCart', $event)"
    />
  </div>
</template>

<style scoped lang="scss "></style>
@/interfaces/Product.interface
