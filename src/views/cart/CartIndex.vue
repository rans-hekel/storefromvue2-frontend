<template>
    <div>
      <div id="page-wrap">
        <h1>Shopping Cart</h1>
        <ItemCart 
        v-for="item in cartItems"
        :key="item.id"
        :item="item"
        v-on:remove-item="removeFromCart($event)"
        />
        <h3 id="total-price">Total : Rp{{ totalPrice }}.000</h3>
        <button id="checkout-button">Checkout</button>
      </div> 
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import ItemCart from '../../components/ItemCart.vue';
  export default {
    components: {
      ItemCart
    },
    data() {
      return {
        cartItems: [ ]
      }
    },
    computed:{
      totalPrice() {
        return this.cartItems.reduce((total, item) => total + Number(item.price), 0)
      }
    },
    methods: {
      async removeFromCart(product) {
        await axios.delete(`http://localhost:3000/api/orders/delete/user/1/product/${product}`)
        let indexCart = this.cartItems.map(function(item) {
          return item.code
        }).indexOf(product)

        this.cartItems.splice(indexCart, 1)
      }
    },
    async created() {
      const result = await axios.get('http://localhost:3000/api/orders/user/1')
      let data = Object.assign({}, 
      ...(result.data.map(
          result => ({ 
            user_id: result.user_id,
            cartItems: result.products, 
          }) 
      ))
    );
      this.cartItems = data.cartItems
    }
  }
  </script>
  
  <style scoped>
  h1 {
    border-bottom: 1px solid #41B883;
    margin: 0;
    margin-top: 16px;
    padding: 16px;
  }
  #total-price {
    padding: 16px;
    text-align: right;
  }
  #checkout-button {
    width: 100%;
  }
  
  </style>