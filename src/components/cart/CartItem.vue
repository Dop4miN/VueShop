<template>
  <div class="cart-item d-flex">
    <h3 class="title">{{ item.title }}</h3>

    <div class="d-flex noselect">
      <div
        class="circle remove position-relative"
        @click.prevent="removeFromCart()"
      >
        <span class="position-absolute">-</span>
      </div>

      <small>&nbsp;{{ item.quantity }}&nbsp;</small>

      <div class="circle add position-relative" @click.prevent="addToCart()">
        <span class="position-absolute">+</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["item"],
  methods: {
    addToCart() {
      this.$store.commit("addToCart", this.item);
    },
    removeFromCart() {
      this.$store.commit("removeFromCart", this.item);
    },
  },
};
</script>

<style scoped lang="scss">
.noselect {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.cart-item {
  border-bottom: 1px solid;
  padding: 1rem;
  justify-content: space-between;
  .title {
    font-size: 1rem;
  }
  .circle {
    border: 1px solid;
    cursor: pointer;
    height: 1rem;
    width: 1rem;
    span {
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }
}
</style>
