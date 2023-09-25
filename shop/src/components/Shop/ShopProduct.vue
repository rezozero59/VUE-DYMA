<script setup lang="ts">
import type { ProductInterface } from '@/interfaces/Product.interface'
defineProps<{
  product: ProductInterface
}>()
const emit = defineEmits<{
  (e: 'addProductToCart', productId: number): void
}>()
</script>

<template>
  <div class="product d-flex flex-column">
    <img :src="product.image" :alt="'Image de ' + product.title" />
    <div class="info-product d-flex flex-column">
      <h4>{{ product.title }}</h4>
      <p>{{ product.description }}</p>
      <div class="d-flex flex-row align-items-center">
        <span class="price flex-fill">Prix: {{ product.price }}€</span>
        <button class="btn btn-primary" @click="emit('addProductToCart', product.id)">
          Ajouter au panier
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss ">
.product{
background-color: #ffffff;
 border:var(--border);
  border-radius: var(--border-radius);
  img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    aspect-ratio: 1/1;
    border-radius: 4px 4px 0 0;




  }
.info-product {
  padding: 10px;


  .price {
    font-weight: bold;

  }
}
}
</style>
@/interfaces/Product.interface
