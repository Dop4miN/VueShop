<template>
  <nav class="d-flex">
    <div class="brand d-flex">Super Fancy Store</div>

    <div class="shopping-cart-wrapper position-relative">
      <div class="icon position-relative" @click.prevent="toggleShowCart()">
        <img class="img-fluid" src="./assets/shopping-cart-icon.png" alt="Shopping Cart" />
        <span v-if="cartItemCounter > 0" class="cartItemCounter position-absolute">{{ cartItemCounter }}</span>
      </div>

      <div id="shopping-cart" class="shopping-cart position-absolute">
        <CartItem v-for="item in items" :key="item.id" :item="item" />

        <CartSummary />
      </div>
    </div>
  </nav>

  <div class="products d-flex">
    <ProductItem v-for="(item, i) in products" :key="i" :product="item" />
  </div>
</template>

<script>
import axios from 'axios';

import CartItem from './components/cart/CartItem.vue'
import CartSummary from './components/cart/CartSummary.vue'
import ProductItem from './components/products/ProductItem.vue'

export default {
    mounted() {
        this.$store.commit('updateCartFromLocalStorage')
    },
    name: "HomeView",
    components: { CartItem, CartSummary, ProductItem },
    data() {
        return {
            products: []
        };
    },
    methods: {
        async getData() {
            try {
                const response = await axios.get(
                    // had to use a different API, since fakestoreapi.com is down
                    "https://api.escuelajs.co/api/v1/products"
                );
                this.products = response.data;
            } catch (err) {
                console.log(err)
            }
        },
        toggleShowCart() {
            document.getElementById('shopping-cart').classList.toggle('active')
        }
    },
    created() {
        this.getData();
    },
    computed: {
        items() {
            return this.$store.getters.cartItems
        },
        cartItemCounter() {
            return this.items.length
        }
    }
}
</script>

<style lang="scss">
// variables
$primary: #ff4800;
$white: #ffffff;

// helper-classes
.img-fluid {
  height: auto;
  width: 100%;
}

.d-flex {
  display: flex;
}

.position-relative {
  position: relative;
}

.position-absolute {
  position: absolute;
}

// customizations
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

html,
body {
  margin: 0;
  padding: 0;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  margin: 0;
}

nav {
  background-color: $primary;
  justify-content: space-between;
  padding: 1rem;
  position: fixed;
  left: 0;
  right: 0;
  z-index: 1;

  .brand {
    align-self: center;
    font-weight: bold;
  }

  .shopping-cart-wrapper {
    .icon {
      cursor: pointer;
      height: 3rem;
      width: 3rem;

      .cartItemCounter {
        top: 0;
        right: 0;
        background-color: #000000;
        border-radius: 100%;
        color: #ffffff;
        height: 1rem;
        width: 1rem;
        padding: 0.1rem;
        text-align: center;
        font-size: 0.75rem;
      }
    }
    .shopping-cart {
        &.active {
            display: block;
        }

      background-color: $white;
      display: none;
      border: 1px solid;
      right: 0;
      width: calc(100vw - 2rem);

      @media (min-width: 500px) {
        width: 27.5rem;
      }
    }
  }
}

.products {
    flex-wrap: wrap;
    justify-content: space-around;
    padding-top: 5rem;
}
</style>
