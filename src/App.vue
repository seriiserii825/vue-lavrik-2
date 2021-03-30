<template>
  <div class="site">
    <header>
      <h1>Site</h1>
      <Cart :price="price" :cnt="cnt"></Cart>
    </header>
    <hr>
    <div class="body">
      <Product
        :price="price"
        @increase="cnt++"
        @decrease="onDecrease"
      ></Product>
    </div>
  </div>
</template>
<script>
import Product from "./components/Product";
import Cart from "./components/Cart";

export default {
  data () {
    return {
      price: 1000,
      cnt: 0
    }
  },
  components: { Cart, Product },
  methods: {
    onDecrease () {
      if (this.cnt > 1) {
        this.cnt--;
      }
    }
  }
}
</script>
<style>
.site {
  text-align: center;
}
</style>
