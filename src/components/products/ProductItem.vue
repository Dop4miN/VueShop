<template>
  <div class="card d-flex position-relative">
    <img
      class="img-fluid product-image"
      :src="product.images[0]"
      :alt="product.title"
    />
    <div class="product-info">
      <h3 class="title">{{ product.title }}</h3>
      <p class="description">{{ product.description }}</p>
      <div class="button" @click.prevent="addToCart()">
        <img
          class="img-fluid icon"
          src="../../assets/shopping-cart-icon.png"
          alt="Shopping Cart"
        />
        ${{ product.price.toFixed(2) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["product"],
  methods: {
    addToCart() {
      this.$store.commit("addToCart", this.product);
    },
  },
};
</script>

<style scoped lang="scss">
.card {
  border: 1px solid;
  width: calc(100% - 2rem);
  margin: 1rem 0;
  flex-direction: column;
  justify-content: space-between;
  overflow: hidden;

  .product-image {
    transition: filter 0.5s;
  }
  .product-info {
    padding: 0.75rem;
    bottom: -100%;
    transition: bottom 0.5s;
    width: calc(100% - 4rem);

    .title {
    }
    .description {
      font-size: 0.85rem;
    }
    .button {
      cursor: pointer;
      background-color: #ff4800;
      color: #000000;
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

      .icon {
        width: 1.75rem;
      }
    }
  }
}

@media (min-width: 500px) {
  .card {
    width: 17.5rem;
    margin: 1rem;
  }
}

@media (min-width: 800px) {
  .card {
    width: 25rem;
    &:hover {
      .product-image {
        filter: blur(3px) brightness(50%);
      }
      .product-info {
        bottom: 0;
      }
    }
    .product-info {
      position: absolute;
      color: #ffffff;
    }
  }
}
</style>
