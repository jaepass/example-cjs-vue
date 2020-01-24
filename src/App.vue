<template>

  <!-- Hero section -->
  <div>
    <div class="hero-wrapper">
            <div class="hero-img-1">
                <div class="logo" href="/">
                    <img width="175px" src="@/assets/logo.png" alt="Tribal Logo">
                </div>
                <div class="hero-text">
                     <a href="/example-cjs-vue/#shop"><p class="discover">discover</p></a>
                     <p>classic timepieces</p>
                </div>
            </div>

            <nav>
                <div class="nav-items">
                <a href="/example-cjs-vue/#cart"><img width="32px" src="@/assets/shopcart-icon.svg" alt="shopping bag icon"></a>
                <p v-if="cartItems.length >= 1" class="text-white">{{ cart.total_items }}</p>
              </div>
          </nav>

            <div class="hero-img-2"></div>
            <div class="hero-img-3"></div>
    </div>

    <!-- Products catalogue -->
    <div class="container mx-auto px-4">
      <div class="flex mb-4">
          <div class="row" id="shop">
          <!-- Loop through products and output -->
          <!-- :key is for Vue to keep track of items with ids -->
            <div class="col-sm-4" v-for="product in products" :key="product.id">
              <!-- Bind product to cart -->
              <product  :product="product"
                        @add-to-cart="addToCart(product)"
                        :isInCart="isInCart(product)"/>  
            </div><!-- END Product Catalogue -->
          </div>
        </div>

        <div class="cart-checkout">
          <!-- Cart container -->
          <div class="cart px-5" id="cart">
            <div class="my-5">
              <cart :items="cartItems"
                    @remove-from-cart="removeFromCart"
                    @generate-checkout="generateCheckout()" />
            </div>
          </div><!-- END Cart Container -->

          <!-- Checkout Form -->
          <div v-if="checkout" class="checkout round-lg py-4 px-4 shadow-sm bg-white rounded mb-20">
              <checkout :checkout="checkout"
                        :commerce="commerce"
                        @confirm-order="confirmOrder" />
          </div><!-- END Checkout form -->
        </div><!-- END Cart/Checkout Container -->

        <!-- Order Confirmation Receipt -->
        <div v-if="order" class="">
          <h2 class="">
            Thank you for shopping!
          </h2>
          <h4 class="">
            Your order number is #{{order.id}}
          </h4>
        </div>
        <!-- END Order Confirmation Receipt Container -->
    
      </div><!-- END of App Container -->
      <Footer />
    </div><!-- END of Storefront -->
</template>

<script>
import Product from "@/components/Product.vue";
import Cart from "@/components/Cart.vue";
import Checkout from "@/components/Checkout.vue";

import Footer from "@/components/Footer.vue";

export default {
  name: "app",
  components: {
    Product, 
    Cart, 
    Checkout,
    Footer
  },
  props: {
    commerce: {
      required: true,
      type: Object
    }
  },
  data() {
    return {
      products: [],
      cart: null,
      checkout: null,
      order: null
    };
  },

  //When Vue app is created, run these functions to fetch data from API
  created() {

    //List all products from store 
    this.commerce.products.list().then((resp) => {
        //Successful response
        this.products = resp.data;
      })
      //Error
      .catch((error) => {
        // eslint-disable-next-line
        console.log(error);
      });

    //Invoke commerce cart method to retrieve cart in session
    this.commerce.cart.retrieve().then((resp) => {
      //Successful response
      this.cart = resp;
    })
      //Error
      .catch((error) => {
        // eslint-disable-next-line
        console.log(error);
      })
  },

  //Declare action methods on object
  methods: {

    //Add products to cart
    addToCart(product) {
      this.commerce.cart.add({
        id: product.id,
        quantity: 1,
      }).then(response => {
        this.cart = response.cart;
      })
    },

    //Check if product added matches item to update "added to cart" on product card
    isInCart(product) {
      const item = this.cartItems.find(item => item.id === product.id);
      if (item) {
        return true;
      }
      return false;
    },

    //Invoke remove from cart method
    removeFromCart(lineItemId){
      this.commerce.cart.remove(lineItemId).then(resp => {
        //Successful
        this.cart = resp.cart;
      })
      //Error
      .catch((error) => {
        // eslint-disable-next-line
        console.log(error);
      });
    },

    //Update items in cart
    // updateCart(product) {
    //   const item = this.cartItems.find(item => item.id === product.id);
    //   if (item) {
    //     return true;
    //   }
    //   return false;
    // },
    
    refreshCart(){
      this.commerce.cart.refresh((resp) => {
        //Successful
          this.cart = resp.cart;
      })
      //Error
      .catch((error) => {
        // eslint-disable-next-line
        console.log(error);
      })
    },

    //Create a checkout token to represent customer's order (returns Checkout id if successful)
    generateCheckout(){
      this.commerce.checkout.generateToken(this.cart.id, {type: 'cart'}).then((checkout) => {
        //Successful
        this.checkout = checkout;
      })
      .catch((error) => {
        // eslint-disable-next-line
        console.log(error);
      });
    },
    
    //Capture Order (returns order object if successful)
    confirmOrder(checkoutId, order){
      this.commerce.checkout.capture(checkoutId, order).then((resp) => {
        //Successful
        this.refreshCart()
        this.checkout = null;
        this.order = resp;
      })
        //Error
        .catch((error) => {
        // eslint-disable-next-line
        console.log(error);
      });
    }

  },
  
  computed: {
    cartItems() {
      return this.cart ? this.cart.line_items : []
    }
  } 
};

</script>

<style>
body {
  font-family: 'Roboto', sans-serif;
}

p, a, label, input, h2, h3, h4{
  letter-spacing: 2px;
}

h4{
  text-transform: uppercase;
  font-size: 18px;
}

.hero-wrapper {
  display: grid;
  grid-template-areas: 
      "img1   nav"
      "img1   img2"
      "img1   img3";
	grid-template-rows: 80px 1fr 1fr;
	grid-template-columns: 55% auto;
  grid-gap: 10px;
  height: 100vh;
}

.hero-img-1{
  background-image: url("./assets/hero-img.jpg");
  grid-area: img1;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
}

.logo{
  padding: 30px 0 0 30px;
  cursor: pointer;
}

.logo img{
  width: 120px;
}

.hero-text{
  position: absolute;
  top: 60%;
  left: 50%;
  transform: translateX(-50%);
  text-align: center;
}

.hero-text a{
  text-decoration: none;
}

.hero-text p{
  color: white;
  text-transform: uppercase;
}

.discover{
  color: white;
  text-transform: uppercase;
  border: 1.5px solid white;
  padding: 9px 20px;
  margin-bottom: 20px;
  transition: all 0.3s ease-in-out;
}

.discover:hover{
  color: #040034;
  background-color: #fff;
}


nav{
  grid-area: nav;
  background: #040034;
  background-size: cover;
  /* position: relative; */
  position: sticky;
}

.nav-items{
  display: flex;
  justify-content: flex-end;
  position: relative;
  padding-top: 10px;
  padding-right: 20px;
  top: 50%;
  transform: translateY(-50%);
}

.nav-items a{
  padding-left: 20px;
  text-decoration: none;
}

.hero-img-2{
  background-image: url("./assets/hero-img2.jpg");
  grid-area: img2;
  background-repeat: no-repeat;
  background-size: cover;
  object-fit: contain;
}

.hero-img-3{
  background-image: url("./assets/hero-img3.jpg");
  grid-area: img3;
  background-repeat: no-repeat;
  background-size: cover;
  object-fit: contain;
}

.cart-checkout{
  display: flex;
  justify-content: space-around;
}

.checkout{
  box-shadow: 0 0 10px rgb(223, 223, 223);
  width: 500px; 
}

  @media only screen and (max-width: 400px){
    .cart-checkout{
      display: block;
    }

    .checkout{
      width: 325px; 
    }
  }

</style>