<template>
  <div class="storefront">
    
  <!-- Hero component contains header -->
  <store-hero></store-hero>

    <div class="container mx-auto px-4">
      <div class="flex mb-4">
        <!-- CATEGORIES OUTPUT TESTING -->
        <!-- <div class="row" v-for="category in categories" :key="category">
          <p>{{ category.name }}</p>
          </div> -->

          <div class="row" id="shop">
          <!-- :key is for Vue to keep track of items with ids -->
            <div class="col-sm-4" v-for="product in products" :key="product.id">
              <product  :isInCart="isInCart(product)"
                        v-on:add-to-cart="addToCart(product)"
                        :isInWishlist="isInWishlist(product)"
                        v-on:add-to-wishlist="addToWishlist(product)"
                        :product="product"></product>  
            </div><!-- END Product Catalogue -->
          </div>
        </div>

        <div class="cart-wishlist">
          <!-- Cart container -->
          <div class="col-md-5 my-5" id="shopping-cart">
            <cart v-on:pay="pay()" v-on:remove-from-cart="removeFromCart($event)" :items="cart"></cart>
          </div>
          <!-- Wishlist container -->
          <div class="col-md-5 my-5" id="wishlist">
            <wishlist v-on:remove-from-wishlist="removeFromWishlist($event)" :items="wishlist"></wishlist>
          </div>
        </div><!-- END Cart/Wishlist Container -->

      </div><!-- END of App Container -->
      
    <store-footer></store-footer>
    </div>
</template>


<script>
import Commerce from '@chec.io/commerce';

import Hero from "@/components/Hero.vue";
import Footer from "@/components/Footer.vue";

// import products from "@/products.json";
import Product from "@/components/Product.vue";
import Cart from "@/components/Cart.vue";
import Wishlist from "@/components/Wishlist.vue";

// Initialize store with public key, store key in variable
const myStore = new Commerce('pk_17054571618e73520760e522b00e08ee196503b14e95c', true);

export default {
  name: "app",
  components: {
    'store-hero': Hero,
    'store-footer': Footer,
    Product, 
    Cart, 
    Wishlist
  },
  data() {
    return {
      wishlist: [],
      cart: [],
      products: []
      // categories:[]
    };
  },

  mounted() {
    //List all products from store 
    myStore.products.list()
      .then((resp) => {
        //console.log(resp);
        this.products = resp.data
      })
      .catch((error) => {
                alert(error);
      }); 

       //Generate token checkout 
      // myStore.checkout.generateToken()
      //   .then((response) => {
      //       this.checkout = response.id; // e.g. chkt_959gvxcZ6lnJ7
      //       // Grab your order confirmation data from `response` and show your customer something nice!
            
      //   })
        
      //   .catch((error) => {
      //           alert(error);
      //   });  

  },
  

  //Declare action methods on object
  methods: {
    //Wishlist methods
    addToWishlist(product) {
      this.wishlist.push(product);
    },
    isInWishlist(product) {
      const item = this.wishlist.find(item => item.id === product.id);
      if (item) {
        return true;
      }
      return false;
    },
    removeFromWishlist(product) {
      this.wishlist = this.wishlist.filter(item => item.id !== product.id);
    },
    //Cart methods
    addToCart(product) {
      this.cart.push(product);
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
    pay(){
      this.cart = [];
      this.checkout = [];
    },
    openCheckoutModal(){

    },
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

.cart-wishlist{
  display: flex;
  justify-content: space-between;
}

</style>