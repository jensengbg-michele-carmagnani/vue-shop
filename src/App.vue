<template>
  <div id="app">
    <header>
      <nav class="nav-bar"></nav>
    </header>
    <section class="cart">
      <p>{{ cart.length }}</p>
    </section>
    <product :premium="premium" @add-to-cart="uppdateCart" @remove-from-cart="removeItem" />
   
  </div>
</template>

<script>
import product from "./components/beginner.vue";

export default {
  name: "App",
  components: {
    product,
  },
  data() {
    return { premium: false, cart: [] };
  },
  methods: {
    uppdateCart(id) {
      this.cart.push(id);
      console.log("element added", this.cart);
    },
    removeItem(id) {
      for (let i = this.cart.length - 1; i >= 0; i--) {
        if (this.cart[i] === id) {
          this.cart.splice(i, 1);
          console.log("element removed", this.cart);
        }
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  .cart {
      margin-right: 25px;
      float: right;
      border: 1px solid #d8d8d8;
      padding: 5px 20px;
    }
}
</style>
