<template>
         <div class="navbar-item has-dropdown is-hoverable" style="margin-left: 41px;">
            
            Корзина ({{ $store.state.cartCount }})     

        <div v-if="$store.state.cart.length > 0" class="navbar-dropdown is-boxed is-right" >
            <a v-for="item in $store.state.cart"
                :key="item.id"
                class="navbar-item"
                href=""
            >
              <img v-bind:src="item.src" style="width:500px;"> <br>
          
             {{ item.item }} x{{ item.quantity }} - ${{ item.totalPrice }} <br> 
                 <pre> </pre>
            </a>
<br>
            
                Итого: $ {{ totalPrice() }} 
          

            <hr class="navbar-divider">
        </div>

        <div v-else class="navbar-dropdown is-boxed is-right">
            <a class="navbar-item" href="">
                Корзина пуста
            </a>
        </div>
    </div>
</template>
<script>
export default {
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
}
</script>

