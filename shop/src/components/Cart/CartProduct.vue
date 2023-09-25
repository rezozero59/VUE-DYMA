<script setup lang="ts">
import type { ProductInterface } from '@/interfaces/Product.interface'

defineProps<{ product: ProductInterface }>()

const emit = defineEmits<{
  (e: 'removeProductFromCart', productId: number): void
}>()
</script>

<template>
  <div class="product d-flex flex-row align-item-center">
    <strong class="flex-fill">{{ product.title }}</strong>

    <span>Prix: {{ product.price }}</span>
    <button class="btn btn-danger" @click="emit('removeProductFromCart', product.id)">
      supprimer
    </button>
  </div>
</template>

<style scoped lang="scss ">
.product{
  background-color: var(--grey-1);
  padding: 10px;
  margin-bottom: 10px;
  border: var(--border);
  border-radius: var(--border-radius);
  strong{
    margin-right: 10px;}
  span{
    margin-right: 10px;
  }
}
</style>
@/interfaces/Product.interface
