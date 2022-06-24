<template>
  <div class="card">
    <img class="img-fluid" :src="product.images[0]" :alt="product.title">
    <h3>{{ product.title }}</h3>
    <p>{{ product.description }}</p>
    <h5 class="price">Price: ${{ product.price.toFixed(2) }}</h5>
    <button class="add" @click.prevent="addToCart()">Add to cart</button>
  </div>
</template>

<script>
export default {
    props: ['product'],
    methods: {
        addToCart() {
            this.$store.commit('addToCart', this.product)
        }
    }
}
</script>

<style lang="scss">
.card {
  border: 1px solid;
  width: 80%;
  margin: 10%;
  padding: 10px;
  h5.price {
    color: gray;
  }
  p.description {
    font-size: 0.85rem;
  }
  p.text-muted {
    color: gray;
  }
}

@media (min-width: 500px) {
  .card {
    width: 30%;
    margin: 10px 0;
  }
}
</style>
