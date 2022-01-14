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
        <span>Cart ({{ calculateTotal }})</span>
    </div>
  </header>
  <router-view :inventory="inventory" :addToCart ="addToCart" />
  <Sidebar
    v-if="showSidebar"
    :toggle= 'toggleSidebar'
    v-model:cart.sync = 'cart'
    v-model:inventory.sync = 'inventory'
    :remoe = 'removeItem'
    :totalQuantity = 'calculateTotal'
    :get-price ='getPrice' />
</template>
<script>

// import Sidebar from './components/Sidebar.vue'
import food from '@/food.json'

export default {
  // componets: [Sidebar],
  data () {
    return {
      showSidebar: false,
      inventory: food,
      cart: {}
    }
  },
  methods: {
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    addToCart (name, index) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += this.inventory[index].quantity
      this.inventory[index].quantity = 0
    },
    removeItem (name) {
      delete this.cart[name]
    },
    getPrice (name) {
      const product = this.inventory.find((p) => {
        return p.name === name
      })
      return product.price.USD
    }
  },
  computed: {
    calculateTotal () {
      const total = Object.entries(this.cart).reduce((acc, curr, index) => {
        return acc + (curr[1] * this.getPrice(curr[0]))
      }, 0)
      return total.toFixed(2)
    }
  }
}
</script>

<style>
</style>
