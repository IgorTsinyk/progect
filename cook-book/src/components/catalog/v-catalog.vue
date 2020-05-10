<template>
  <div class="v-catalog">
    <router-link :to="{name: 'cart', params: {cart_data: CART}}">
      <div class="v-catalog-link_to_cart">
        Корзина: {{CART.length}}
      </div>
    </router-link>
    <h3>Солодка сторінка</h3>
    <v-select 
      :selected="selected"
      :options="categories"
      @select="sortByCategories"
    />
    <div class="v-catalog__list">
      <v-catalog-item 
      v-for="product in filteredProducts" 
      :key="product.article" 
      :product_data="product" 
      @addToCart="addToCart"
      />
    </div>
  </div>
</template>

<script>
import vCatalogItem from "./v-catalog-item";
import {mapActions, mapGetters} from 'vuex'
import vSelect from '../v-select'

export default {
  data() {
    return {
      categories: [
        {name: 'Всі', value: 'All'},
        {name: 'Торти', value: 'т'},
        {name: 'Печиво', value: 'п'}
      ],
      selected: 'Всі',
      sortedProducts: []
    };
  },
  name: "v-catalog",
  components: {
    vCatalogItem,
    vSelect
  },
  props: {},
  computed: {
    ...mapGetters([
      'PRODUCTS',
      'CART'
      ]),
      filteredProducts(){
        if(this.sortedProducts.length){
          return this.sortedProducts
        } else {
           return this.PRODUCTS
        }
      }
  },
  methods: {
    ...mapActions([
      'GET_PRODUCTS_FROM_API',
      'ADD_TO_CART'
      ]),

      sortByCategories(category){
        this.sortedProducts = []
        let vm = this
         this.PRODUCTS.map(function(item){
           if(item.category === category.name){
             vm.sortedProducts.push(item)
           }
         })
      },
     addToCart(data){
       this.ADD_TO_CART(data)
     }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API()
  }
};
</script>

<style >
.v-catalog__list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
}
.v-catalog-link_to_cart{
  position: absolute;
  top: 10px;
  right: 10px;
  padding: 16;
  border: solid 1px;
  }

</style>