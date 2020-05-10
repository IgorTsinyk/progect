<template>
  <div class="v-cart">
    <router-link :to="{name: 'catalog'}">
      <div class="v-catalog-link_to_cart">
        Повернутись на сторінку
      </div>
    </router-link>
    <h3>Корзина</h3>
    <p v-if="!cart_data.length">Корзина порожня</p>
    <v-cart-item 
      v-for="(item, index) in cart_data"
      :key="item.article"
      :cart_item_data="item"
      @deleteFromCart="deleteFromCart(index)"
      @increment="increment(index)"
      @decrement="decrement(index)"
    />
    <div class="v-cart-total">
      <p class="total-name">Total: </p>
      <p>{{cartTotalCost}}</p>
    </div>
  </div>
</template>

<script>
import vCartItem from "./v-cart-item"
import {mapActions} from 'vuex'
export default {
  name: "v-cart",
  components: {
    vCartItem
  },
  
  props: {
    cart_data: {
      type: Array,
      default() {
        return []
      }
    }
  },

  data() {
    return{}
  },

  computed: {
    cartTotalCost() {
      let result = []
      if (this.cart_data.length){
          for (let item of this.cart_data){
            result.push(item.price*item.quantity) 
          }
            result = result.reduce(function(sum, el){
            return sum+el
          })
         
      return result
      }
      else {
        return 0
      }
    }
  },
  methods: {
    ...mapActions([
      'DELETE_FROM_CART',
      'INCREMENT_CART_ITEM',
      'DECREMENT_CART_ITEM'
    ]),
    increment(index){
      this.INCREMENT_CART_ITEM(index)
    },
    decrement(index){
      this.DECREMENT_CART_ITEM(index)
    },
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index)
    }
  }
};
</script>

<style>
  .v-cart-total{
    position: fixed;
    bottom: 0;
    right: 0;
    left: 0;
    padding: 24 24;
    display: flex;
    justify-content: center;
    background: rgb(209, 74, 24);
    color: rgb(218, 215, 53);
    font-size: 20px;
  }
  .total-name{
    margin-right: 18 ;
  }
</style>