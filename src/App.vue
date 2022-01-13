<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>
    <div
    @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart 0</span>
      <!-- <span>Cart ({{ totalQuantity }})</span> -->
    </div>
  </header>
  <router-view :inventory="inventory" />
  <Sidebar
    v-if="showSidebar"
    :toggle= 'toggleSidebar'
    :cart = 'cart'
    :inventory = 'inventory'
    :remoe = 'remove' />
</template>
<script>

import Sidebar from './components/Sidebar.vue'
import food from '@/food.json'

export default {
  componets: [Sidebar],
  data () {
    return {
      showSidebar: true,
      inventory: food,
      cart: {}
    }
  },
  methods: {
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    }
  }
}
</script>

<style>
</style>
