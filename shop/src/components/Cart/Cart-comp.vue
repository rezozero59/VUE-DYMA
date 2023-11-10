<script setup lang="ts">
import { computed } from 'vue'
import type { ProductCartInterface } from '@/interfaces'
import CartProductList from './CartProductList.vue'

const props = defineProps<{
  cart: ProductCartInterface[]
}>()

const totalPrice = computed(() =>
  props.cart.reduce((acc, product) => {
    return acc + product.price * product.quantity
  }, 0)
)

const emit = defineEmits<{
  (e: 'removeProductFromCart', productId: number): void
}>()
</script>

<template>
  <div class="container d-flex flex-column">
    <h2 class="title">Panier</h2>
    <cart-product-list
      :cart="cart"
      @remove-product-from-cart="emit('removeProductFromCart', $event)"
    />
    <button class="btn btn-success">Commander ({{ totalPrice }}€)</button>
  </div>
</template>

<style scoped lang="scss ">

.container {
  padding: 20px;
}
</style>
