<template>
    <div class="v-cart-item">
        <img class="v-cart-item__image" :src="require('../../assets/' + cart_item_data.image)" alt="item" />
        <div class="v-cart-item-info">
            <p>{{cart_item_data.name}}</p>
            <p>{{cart_item_data.price}}</p>
            <p>{{cart_item_data.article}}</p>
        </div>
        <div 
            class="cart_item_quantity">
            <p>Кількість: </p>
            <span>
                <span class="quantity-btn" @click="decrementItem">-</span>
                {{cart_item_data.quantity}}
                <span class="quantity-btn" @click="incrementItem">+</span>
            </span> 
        </div>
        <button @click="deleteFromCart">Delete</button>
    </div>
</template>

<script>

    export default {
        name: "v-cart-item",
        props: {
            cart_item_data: {
                type: Object,
                default() {
                    return {}
                }
            }
        },
        data() {
            return{}
        },
        computed: {},
        methods:{
            decrementItem(){
                this.$emit('decrement')
            },
            incrementItem(){
                this.$emit('increment')
            },

            deleteFromCart() {
                this.$emit('deleteFromCart')
            }
        },
        mounted() {
            this.$set(this.cart_item_data, 'quantity', 1)
        }
    }
</script>

<style >
.v-cart-item{
    display: flex;
    flex-wrap: nowrap;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 0 8px 0 #c0c0c0;
    padding: 16;
    margin-bottom: 16;
}
.quantity-btn{
    cursor: pointer;
}
</style>