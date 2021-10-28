<template>
    <div class="products">
        <form class="searchbar">
            <input placeholder="Пошук" v-model="search">
            <input type="submit"  class="btn">
        </form>
        <td>
 
</td>
        <div class="product" v-for="(item) in filteredItems" v-bind:key="item.id">
            <div class="product-image">
                <img v-bind:src="item.src">
            </div>
            <div>
                <h4 class="product-title">
                    <router-link v-bind:to="'/product/' + item.id">
                        {{ item.item }}
                    </router-link>
                </h4>
                <label>{{item.price}}</label>
                  <button class="btn"
        v-on:click="addToCart(item)">Add to Cart</button>
            </div>
        </div>

        <div class="navbar-item has-dropdown is-hoverable">
            
    <router-link v-bind:to="'/cart/'">
            Корзина ({{ $store.state.cartCount }})
       </router-link>
        

    </div>
    </div>

    
</template>
<script>
    import products from '../data/products.js'

    export default {
        data: function () {
            return {
                items: [],
                search: '',
                searchResult: []
            };
        },
        mounted: function(){
            this.items = products;
        },
        methods: {
            addToCart(item) {
                this.$store.commit('addToCart', item);
            },
            totalPrice() {
                let sum = 0
                let cart =  this.$store.state.cart
                cart.forEach ( (item) => {
                        sum += item.totalPrice;
                    
                });
                return sum;
            }
},
        computed: {
            filteredItems: function() {
                console.log(this);
                if (!this.search) {
                    return this.items;
                }
                return this.items.filter(element => {
                    return element.item.toUpperCase().includes(this.search.toUpperCase());
                });
            },
            getCart: function() {
                console.log(this.$store.getters.getCart)
                return this.$store.getters.getCart
            }
        }
    }
</script>
