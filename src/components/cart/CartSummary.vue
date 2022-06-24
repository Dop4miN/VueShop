<template>
  <div class="cart-summary">
    <div v-if="items" class="cart-item-card">
      <h3>Total: ${{ cart_total.toFixed(2) }}</h3>

      <button>Proceed to checkout</button>
    </div>

    <div v-else>No items in your shopping cart.</div>
  </div>
</template>

<script>
export default {
    computed: {
        cart_total() {
            return this.$store.getters.cartItems.reduce((a, b) => a + (b.price * b.quantity), 0)
        },
        items() {
            return this.$store.getters.cartItems.length > 0
        }
    }
}
</script>

<style scoped lang="scss">
.cart-summary {
  padding: 1rem;
  h3 {
    margin-bottom: 1rem;
  }
  button {
    cursor: pointer;
    background-color: #ff4800;
    border: none;
    padding: 0.75rem 1.25rem;
    text-align: center;
    transition: background-color 0.2s;
    font-size: 1.25rem;
    font-weight: bold;
    width: 100%;
    &:hover {
      background-color: darken(#ff4800, 10%);
    }
  }
}
</style>
