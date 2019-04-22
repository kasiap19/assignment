<template>
  <div id="app">
    <Header/>
    <Products :products="products" />
  </div>
</template>

<script>
import Products from './components/Products.vue';
import Header from './components/Header.vue';

export default {
  name: 'app',
  components: {
    Products,
    Header
  },

  data() {
    return {
      products: [],
    }
  },

  created () {
    fetch('https://5c78274f6810ec00148d0ff1.mockapi.io/api/v1/products')
        .then(response => response.json())
        .then((data) => {
        this.products = data;

        // console.log(this.products)
    });
  },
};
</script>

<style lang="scss">
@import 'assets/_settings.scss';

#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
