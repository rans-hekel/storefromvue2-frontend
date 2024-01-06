<template>
    <div>
      <div id="page-wrap" v-if="product">
        <div id="img-wrap">
          <img :src="product.imageUrl" :alt="product.name">
        </div>
        <div id="product-details">
          <h1>{{ product.name }}</h1>
          <h3 id="price">Rp. {{ product.price }}</h3>
          <p>Average rating: {{ product.averageRating }}</p>
          <button id="add-to-cart">Add To Cart</button>
          <p>{{ product.description }}</p>
        </div>
      </div>
      <NotFound v-else/>
    </div>
  </template>
  
  <script>
  import { products } from '../../data-seed';
  import NotFound from '../errors/NotFound.vue';
  export default {
    components: {
      NotFound
    },
  data() {
    return {
      products
    }
  },
  computed: {
    product() {
      return this.products.find(product => product.id === this.$route.params.id)

    }
  },
  mounted() {
    console.log(this.product)
  }
  }
  </script>
  
  <style scoped>
  #page-wrap {
    margin-top: 16px;
    padding: 16px;
    max-width: 600px;
  }

  #img-wrap {
    text-align: center;;
  }

  img {
    width: 400px;
  }

  #product-details {
    padding: 16px;
    position: relative;
  }

  #add-to-cart {
    width: 100%;
  }

  #price {
    position: absolute;
    top: 24px;
    right: 16px;
  }
  .notif {
    text-align: center;
    color: white;
    background-color:#41B883;
    padding: 3%;
    border-radius: 8px;
  }
  </style>