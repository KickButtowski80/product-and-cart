<template>
  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
        <span>
          Cart
          <i class="icofont-cart-alt icofont-1x"></i>
        </span>
        <button class="cart-close" @click="toggle">&times;</button>
      </h1>

      <div class="cart-body">
        <table class="cart-table">
          <thead>
            <tr>
              <th><span class="sr-only">Product Image</span></th>
              <th>Product</th>
              <th>Price</th>
              <th>Qty</th>
              <th>Total</th>
              <th><span class="sr-only">Actions</span></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(quantity, key, i) in cart" :key="i">
              <td><i class="icofont-carrot icofont-3x"></i></td>
              <td>{{ key }}</td>
              <td>${{ getPrice(key) }}</td>
              <td class="center">{{ quantity }}</td>
              <td>${{ quantity * getPrice(key) }}</td>
              <td class="center">
                <button @click="remove(key)" class="btn btn-light cart-remove">
                  &times;
                </button>
              </td>
            </tr>
          </tbody>
        </table>

        <p class="center"><em>No items in cart</em></p>
        <div class="spread">
          <span><strong>Total:</strong> ${{totalQuantity}}</span>
          <button class="btn btn-light">Checkout</button>
        </div>
      </div>
    </div>
  </aside>
</template>
<script>
export default {
  props: ['toggle', 'cart', 'inventory', 'remove', 'totalQuantity', 'getPrice'],
  methods: {
    // getPrice (name) {
    //   const product = this.inventory.find((p) => {
    //     return p.name === name
    //   })
    //   return product.price.USD
    // }
  },
  mounted () {
    // Instead of calling the method we emit an event
    console.log('get price ', this.getPrice)
    this.$emit('get-price', this.getPrice)
  }
}
</script>
