<template>
  <div id="app">
    <nav>
      <router-link :to="{name: 'product'}">Product</router-link> |
      <router-link :to="{name: 'product-detail', params: {id: 1}}">Detail</router-link> |
      <router-link :to="{name: 'cart'}">Shopping Cart</router-link> |
    </nav>
    <router-view/>
  </div>
</template>

<style>
* {
    box-sizing: border-box;
    font-family: Arial;
  }

  #page-wrap {
    margin: auto;
    max-width: 800px;
    min-height: 100vh;
  }

  button {
    background-color: #41B883;
    border: none;
    border-radius: 8px;
    color: white;
    cursor: pointer;
    font-size: 16px;
    font-weight: bold;
    outline: 0;
    padding: 16px;
  }
</style>
