<template>
  <div id="app">
    <breakfast-studio
      :kitchens="kitchens"
      @cartParent="cartHandler"
      :totalMenu="countOfMenuCart"
      :quantityCart="totalQuantityOfMenuCart"
      :cart="cart"
      @removeQuantityParent="removeCartHandler"
    />
    <!-- <BreakfastStudio
      v-for="kitchen in kitchens"
      :key="kitchen.name"
      :name="kitchen.name"
      :image="kitchen.image"
      :groups="kitchen.groups"
    ></BreakfastStudio> -->
    <!-- <BreakfastStudio /> -->
  </div>
</template>

<script>
import BreakfastStudio from "./components/BreakfastStudio";
import DUMMY_DATA from "./kitchen.js";

export default {
  name: "App",
  data: function () {
    return {
      kitchens: DUMMY_DATA,
      cart: [],
      totalqQuantity: 0,
    };
  },
  computed: {
    countOfMenuCart() {
      return this.cart.length;
    },
    totalQuantityOfMenuCart() {
      let total = 0;
      if (this.countOfMenuCart > 0) {
        total = this.cart.reduce((prevState, currentState) => {
          return prevState + currentState.quantity;
        }, 0);
      }
      // console.log(total);
      return total;
    },
  },
  methods: {
    cartHandler(data) {
      // let quantity = 0;
      // const result = this.kitchens.find(menu => menu.name === data.name)
      // if(result) {
      //   quantity += 1;
      //   result['quantity'] = quantity;
      // }
      // console.log(result);
      let quantity = 0;
      
      quantity += 1;
      const result = { ...data, quantity };
      if (this.cart.length <= 0) {
        this.cart.push(result);
        // console.log('quantity :' + quantity);
      } else if (this.cart.length > 0) {
        const findCartIndex = this.cart.findIndex(
          (cart) => cart.name === result.name
        );
        // console.log(findCartIndex);

        if (findCartIndex !== -1) {
          quantity = this.cart[findCartIndex].quantity += 1;
          this.cart[findCartIndex] = { ...data, quantity };
          // console.log('quantity :' + quantity);
          // quantity = 0
        } else {
          quantity = 0;
          quantity += 1;
          // console.log('quantity :' + quantity);
          this.cart[this.cart.length] = { ...data, quantity };
        }
      }
      console.log(this.cart);
    },
    removeCartHandler: function(data) {
      const menu = this.cart.find(cart => cart.name === data.name);
      if(menu) {
menu.quantity -= 1;
      this.cart = this.cart.filter(cart => cart.quantity !== 0);
      }
      
      console.log(this.cart);
    }
  },
  updated: function () {
    // console.log('total quantity ', this.totalQuantityOfMenuCart);
    console.log(this.totalQuantityOfMenuCart);
  },
  provide: function() {
    return {
      cartProvide: this.cart
    }
  },
  components: {
    BreakfastStudio,
  },
};
</script>
 