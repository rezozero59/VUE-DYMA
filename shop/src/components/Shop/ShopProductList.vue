<script setup lang="ts">
import type { ProductInterface } from '@/interfaces'
import ShopProduct from './ShopProduct.vue'

defineProps<{
  products: ProductInterface[]
}>()
const emit = defineEmits<{
  (e: 'addProductToCart', productId: number): void
}>()
</script>

<template>
  <div class="grid">
    <shop-product
      v-for="product in products"
      :key="product.id"
      :product="product"
      @add-product-to-cart="emit('addProductToCart', $event)"
    />
  </div>
</template>

<style scoped lang="scss ">
.grid {
  display: grid;
  grid-template-columns:1fr 1fr 1fr 1fr;
  grid-auto-rows: 400px;
  gap:20px;
  padding: 20px;
}
</style>
@/interfaces/Product.interface
