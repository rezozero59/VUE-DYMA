<script setup lang="ts">
import type { ProductInterface } from '@/interfaces'
import ShopProductList from './ShopProductList.vue'

defineProps<{
  products: ProductInterface[]
}>()

const emit = defineEmits<{
  (e: 'addProductToCart', productId: number): void
}>()
</script>

<template>
  <div>
    <shop-product-list
      @add-product-to-cart="emit('addProductToCart', $event)"
      :products="products"
    />
  </div>
</template>

<style scoped lang="scss "></style>
@/interfaces/Product.interface
