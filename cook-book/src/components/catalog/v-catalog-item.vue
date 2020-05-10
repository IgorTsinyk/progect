<template>
  <div class="v-catalog-item">

    <popup 
      v-if="isInfoPopupVisible"
      rightBtnTitle="Add to cart"
      :closePopup="closeInfoPopup"
      rightBtnAction="addToCart"
    >
    <div>
     <img class="v-catalod-item_image"
    :src="require('../../assets/' + product_data.image)" alt="item" />
    <p class="v-catalog-item_name">{{product_data.name}}</p>
    <p class="v-catalog-item_price">Price: {{product_data.price}}</p>
    </div>
    </popup>

    <img class="v-catalod-item_image"
    :src="require('../../assets/' + product_data.image)" alt="item" />
    <p class="v-catalog-item_name">{{product_data.name}}</p>
    <p class="v-catalog-item_price">Price: {{product_data.price}}</p>
    <button 
      class="show-info"
      @click="showPopup">
      Більше
    </button>
    <button 
    class="v-catalog-item_btn"
    @click="addToCart"
    >Додати до корзини
    </button>
  </div>
</template>

<script>
import popup from '../catalog/popup/v-popup'

export default {
  name: "v-catalog-item",
  components: {
    popup
    },
  props: {
    product_data: {
      type: Object,
      default() {
        return {};
      }
    }
  },
  data(){
    return {
      isInfoPopupVisible: false
    }
  },
  methods: {
    addToCart() {
      this.$emit("addToCart",this.product_data);
    },
    showPopup() {
      this.isInfoPopupVisible = true
    },
    closeInfoPopup(){
      this.isInfoPopupVisible = false
    }
  }
  
};
</script>

<style >
.v-catalog-item {
  flex-basis: 25%;
  box-shadow: 0 0 8px 0 #c0c0c0;
  padding: 16px;
  margin-bottom: 16px;
  width: 100 px;
}
button{
  padding: 8px 16px;
  background: darkgoldenrod;
  color: antiquewhite;
  border: 0;
  border-radius: 8px;
}
</style>