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

          <div class="row">
          <!-- :key is for Vue to keep track of items with ids -->
            <div class="col-sm-4" v-for="product in products" :key="product.id">
              <product  :isInCart="isInCart(product)"
                        v-on:add-to-cart="addToCart(product)"
                        :isInWishlist="isInWishlist(product)"
                        v-on:add-to-wishlist="addToWishlist(product)"
                        :product="product"></product>  
            </div>
          </div>
        </div>
        <div class="cart-wishlist">
          <!-- Cart modal -->
          <div class="col-md-5 my-5">
            <cart v-on:pay="pay()" v-on:remove-from-cart="removeFromCart($event)" :items="cart"></cart>
          </div>
          <!-- Wishlist modal -->
          <div class="col-md-5 my-5" id="wishlist">
            <wishlist v-on:remove-from-wishlist="removeFromWishlist($event)" :items="wishlist"></wishlist>
          </div>
        </div><!-- END Cart/Wishlist Container -->

      </div><!-- END of Container -->
      
    <store-footer></store-footer>
    </div>
</template>


<script>
import Commerce from '@chec.io/commerce';

import Hero from "@/components/Hero.vue";
import Footer from "@/components/Footer.vue";

import products from "@/products.json";
import Product from "@/components/Product.vue";
import Cart from "@/components/Cart.vue";
import Wishlist from "@/components/Wishlist.vue";


// Initialize store with public key, store key in variable myStore
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
      products, 
      wishlist: [],
      cart: []
      // categories:[]
    };
  },

  mounted() {
    //List all products from chec 
    myStore.products.list()
      .then((resp) => {
        //console.log(resp);
        this.products = resp.data
      })
      .catch((error) => {
                alert(error);
            });  
  },

  //Declare action methods on object
  methods: {
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
    pay() {
      this.cart = [];
      alert("Thanks! Shopping successfully completed. ");
    }
  } 
};

</script>

<style>
body {
  background-color: #ffffff;
  font-family: 'Roboto', sans-serif;
}

h1, h2, h3, h4{
  text-transform: uppercase;
}

p, a{
  letter-spacing: 2.5px;
}

.cart-wishlist{
  border: 1px solid red;
  display: flex;
  justify-content: space-between;
}

</style>