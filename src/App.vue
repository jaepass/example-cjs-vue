<template>
  <div class="storefront">
    <nav>
        <a href="/example-cjs-vue/#shopping-cart"><img width="32px" src="@/assets/bag-icon.svg" alt="shopping bag icon"></a>
        <p v-if="cartItems.length >= 1">{{ cart.total_items }}</p>
    </nav>
    <!-- <p>{{message.text}}</p> -->

    <div class="container mx-auto px-4">
      <div class="flex mb-4">

          <div class="row" id="shop">
          <!-- Loop through products and display -->
          <!-- :key is for Vue to keep track of items with ids -->
            <div class="col-sm-4" v-for="product in products" :key="product.id">
              <!-- Bind product to cart -->
              <product  :product="product"
                        @add-to-cart="addToCart(product)"
                        :isInCart="isInCart(product)"/>  
            </div><!-- END Product Catalogue -->
          </div>
        </div>

        <div class="cart-checkout row">

          <!-- Shopping Cart container -->
          <div class="cart">
            <div class="col-sm-4 my-5" id="shopping-cart">
              <cart :items="cartItems"
                    @remove-from-cart="removeFromCart"
                    @generate-checkout="generateCheckout()" />
            </div>
          </div><!-- END Cart Container -->

          <!-- Checkout Form -->
          <div v-if="checkout" class="checkout">
            <div class="col-sm-8 my-5" id="checkoutForm">
              <checkout :checkout="checkout"
                        :commerce="commerce"
                        @confirm-order="confirmOrder" />
            </div>
          </div><!-- END Checkout form -->

        </div><!-- END Cart/Checkout Container -->

        <!-- Order Confirmation Receipt -->

        <!-- END Order Confirmation Receipt Container -->
    

      </div><!-- END of App Container -->
    </div><!-- END of Storefront -->
</template>

<script>
import Product from "@/components/Product.vue";
import Cart from "@/components/Cart.vue";
import Checkout from "@/components/Checkout.vue";

export default {
  name: "app",
  components: {
    Product, 
    Cart, 
    Checkout
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
      message: {},
      cart: null,
      checkout: null
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
          alert(error);
      });

    //Invoke commerce cart method to retrieve cart in session
    this.commerce.cart.retrieve().then((resp) => {
      if (!resp.error) {
        this.cart = resp;
      }
    });
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
        //alert("added to cart!")
      })
    },

    //Check if product added matches item to update "added to cart" change on product card
    isInCart(product) {
      const item = this.cartItems.find(item => item.id === product.id);
      if (item) {
        return true;
      }
      return false;
    },

    //Invoke remove from cart method
    removeFromCart(lineItemId){
      this.commerce.cart.remove(lineItemId, (resp) => {
        if(!resp.error){
          this.cart = resp.cart;
        }
      })
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
        // Error
        if(!resp.error){
          this.cart = resp.cart;
        }
      })
    },

    // removeFromCart(product) {
    //   this.commerce.cart = this.cart.filter(item => item.id !== product.id);
    // },
    // pay(){
    //   this.cart = [];
    // },

    //Create a checkout token to represent customer's order (Capture the order to process in checkout)
    generateCheckout(){
      this.commerce.checkout.generateToken(this.cart.id, {type: 'cart'}).then((checkout) => {
        this.checkout = checkout;
      })
      .catch((error) => {
        alert(error);
      });
    },
    
    //Capture Order
    confirmOrder(){

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
  background-color: #ffffff;
  font-family: 'Roboto', sans-serif;
}

p, a{
  letter-spacing: 2px;
}

nav{
  display: flex;
  position: fixed;
  top: 20px;
  right: 40px;
  z-index: 999;
}

nav p{
  padding-top: 5px;
}

.cart-checkout{
  border: 1px solid red;
  display: flex;
}

/* .cart{

} */

</style>