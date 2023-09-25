<script setup lang="ts">
import HeaderComp from './components/Header-comp.vue'
import ShopComp from './components/Shop/Shop-comp.vue'
import CartComp from './components/Cart/Cart-comp.vue'
import FooterComp from './components/Footer-comp.vue'
import data from './data/products'

import { reactive } from 'vue'
import type { ProductInterface, ProductCartInterface } from './interfaces'

const state = reactive<{
  products: ProductInterface[]
  cart: ProductCartInterface[]
}>({
  products: data,
  cart: []
})

// Fonction pour ne pas afficher deux fois le même produit dans le panier
function addProductToCart(productId: number): void {
  const product = state.products.find((product) => product.id === productId)
  if (product && !state.cart.find((product) => product.id === productId)) {
    state.cart.push({ ...product, quantity: 1 })
  }
}

function removeProductFromCart(productId: number): void {
  state.cart = state.cart.filter((product) => product.id !== productId)
}
</script>

<template>
  <div class="app-container">
    <header-comp class="header" />
    <shop-comp :products="state.products" @add-product-to-cart="addProductToCart" class="shop" />
    <cart-comp :cart="state.cart" class="cart" @remove-product-from-cart="removeProductFromCart" />
    <footer-comp class="footer" />
  </div>
</template>

<style lang="scss ">
@import './assets/base.scss';
@import './assets/debug.scss';

.app-container {
  min-height: 100vh;
  display: grid;
  grid-template-areas:'header header'
                      'shop cart'
                      'footer footer';
  grid-template-columns: 75% 25%;
  grid-template-rows: 48px auto 48px;
}

.header {
  grid-area: header;
}

.shop {
  grid-area: shop;
}

.cart {
  grid-area: cart;
  border-left: var(--border);
  background-color: #ffffff;
}

.footer {
  grid-area: footer;
}
</style>
./interfaces/Product.interface
