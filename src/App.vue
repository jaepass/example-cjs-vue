<template>
  <div class="storefront">

    <div class="container mx-auto px-4">
      <div class="flex mb-4">

          <div class="row" id="shop">
          <!-- Loop through products and display -->
          <!-- :key is for Vue to keep track of items with ids -->
            <div class="col-sm-4" v-for="product in products" :key="product.id">
              <product  :isInCart="isInCart(product)"
                        v-on:add-to-cart="addToCart(product)"
                        :product="product"></product>  
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
    //Create cart object
    commerce.cart.retrieve((cart) => {
          if (!cart.error) {
            this.cart = cart;
          }
        });
  },
  
  //Declare action methods on object
  methods: {
    //Cart methods

    //Add products to cart
    addToCart(product) {
      //this.cart.push(product);
      commerce.cart.add(product);
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

.cart{
  display: flex;
  justify-content: space-between;
}

</style>