<template>
  <div class="storefront">

    <nav>
        <a href="/example-cjs-vue/#shopping-cart"><img width="32px" src="@/assets/bag-icon.svg" alt="shopping bag icon"></a>
    </nav>

    <div class="container mx-auto px-4">
      <div class="flex mb-4">

          <div class="row" id="shop">
          <!-- Loop through products and display -->
          <!-- :key is for Vue to keep track of items with ids -->
            <div class="col-sm-4" v-for="product in products" :key="product.id">
              <!-- Bind product to cart -->
              <product  :isInCart="isInCart(product)"
                        v-on:add-to-cart="addToCart(product)"
                        :product="product" />  
            </div><!-- END Product Catalogue -->
          </div>
        </div>

        <div class="cart">
          <!-- Cart container -->
          <div class="col-md-5 my-5" id="shopping-cart">
            <cart v-on:pay="pay()" v-on:remove-from-cart="removeFromCart($event)" :items="cart"></cart>
          </div>
        </div><!-- END Cart Container -->

      </div><!-- END of App Container -->
      
    </div>
</template>

<script>
import Commerce from '@chec.io/commerce';

import Product from "@/components/Product.vue";
import Cart from "@/components/Cart.vue";

// Initialize store with public key, store key in variable
const commerce = new Commerce('pk_17054571618e73520760e522b00e08ee196503b14e95c', true);

export default {
  name: "app",
  components: {
    Product, 
    Cart, 
  },
  data() {
    return {
      cart: [],
      products: []
    };
  },

  //When Vue app is created, run these functions to fetch data from API
  created() {
    //List all products from store 
    commerce.products.list()
      .then((resp) => {
        //Successful response
        this.products = resp.data
      })
      //Error
      .catch((error) => {
          alert(error);
      });

      // invoke commerce cart method to retrieve cart in session
      commerce.Cart.retrieve((cart) => {
        if (!cart.error) {
          this.cart = cart;
        }
      });
   
    //Will use cart id in current session
    // Commerce.Cart.retrieve((resp) => { 
    //   return resp;
    // });
  },
  
  //Declare action methods on object
  methods: {
    //Cart methods

    //Add products to cart
    addToCart(product) {
      this.cart.push(product);
      //commerce.cart.push(product);
    },
    isInCart(product) {
      const item = this.cart.find(item => item.id === product.id);
      if (item) {
        return true;
      }
      return false;
    },
    
    removeFromCart(product) {
      this.cart = this.cart.filter(item => item.id !== product.id);
    },
    // pay(){
    //   this.cart = [];
    //   this.checkout = [];
    // },
    // openCheckoutModal(){

    // },
  } 
};

</script>

<style>
body {
  background-color: #ffffff;
  font-family: 'Roboto', sans-serif;
}

p, a{
  letter-spacing: 2px;
}

nav img{
  display: flex;
  position: fixed;
  top: 20px;
  right: 40px;
  z-index: 999;
}

.cart{
  display: flex;
  justify-content: space-between;
}

</style>