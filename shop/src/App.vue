<script setup lang="ts">
import HeaderComp from './components/Header-comp.vue'
import ShopComp from './components/Shop/Shop-comp.vue'
import CartComp from './components/Cart/Cart-comp.vue'
import FooterComp from './components/Footer-comp.vue'
import data from './data/products'

import { reactive, computed } from 'vue'
import type {
  ProductInterface,
  ProductCartInterface,
  FiltersInterface,
  FilterUpdate
} from './interfaces'
import { DEFAULT_FILTERS } from './data/filters'

const state = reactive<{
  products: ProductInterface[]
  cart: ProductCartInterface[]
  filters: FiltersInterface
}>({
  products: data,
  cart: [],
  filters: { ...DEFAULT_FILTERS }
})

function addProductToCart(productId: number): void {
  const product = state.products.find((product) => product.id === productId)
  if (product) {
    const productInCart = state.cart.find((product) => product.id === productId)
    if (productInCart) {
      productInCart.quantity++
    } else {
      state.cart.push({ ...product, quantity: 1 })
    }
  }
}
// Fonction à relire et analyser
function removeProductFromCart(productId: number): void {
  const productFromCart = state.cart.find((product) => product.id === productId)
  if (productFromCart) {
    if (productFromCart.quantity > 1) {
      productFromCart.quantity--
    } else {
      state.cart = state.cart.filter((product) => product.id !== productId)
    }
  }
}

function updateFilter(filterUpdate: FilterUpdate) {
  if (filterUpdate.search !== undefined) {
    state.filters.search = filterUpdate.search
  } else if (filterUpdate.priceRange !== undefined) {
    state.filters.priceRange = filterUpdate.priceRange
  } else if (filterUpdate.category !== undefined) {
    state.filters.category = filterUpdate.category
  } else {
    state.filters = { ...DEFAULT_FILTERS }
  }
}

const cartEmpty = computed(() => state.cart.length === 0)
const filteredProducts = computed(() => {
  return state.products.filter((product) => {
    if (
      product.title.toLocaleUpperCase().startsWith(state.filters.search.toLocaleUpperCase()) &&
      product.price >= state.filters.priceRange[0] &&
      product.price <= state.filters.priceRange[1] &&
      (product.category === state.filters.category || state.filters.category === 'all')
    ) {
      return true
    } else {
      return false
    }
  })
})
</script>

<template>
  <div class="app-container" :class="{ gridEmpty: cartEmpty }">
    <header-comp class="header" />
    <shop-comp
      :products="filteredProducts"
      :filters="state.filters"
      @add-product-to-cart="addProductToCart"
      class="shop"
      @update-filter="updateFilter"
    />
    <cart-comp
      v-if="!cartEmpty"
      :cart="state.cart"
      class="cart"
      @remove-product-from-cart="removeProductFromCart"
    />
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

.gridEmpty {
  grid-template-areas:'header header'
                      'shop shop'
                      'footer footer';
  grid-template-columns: 100%;
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
