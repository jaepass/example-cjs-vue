<template>
  <div class="storefront">

    <nav>
        <a href="/example-cjs-vue/#shopping-cart"><img width="32px" src="@/assets/bag-icon.svg" alt="shopping bag icon"></a>
        <p v-if="cart.length >= 1">{{ cart.length }}</p>
    </nav>

    <div class="container mx-auto px-4">
      <div class="flex mb-4">

          <div class="row" id="shop">
          <!-- Loop through products and display -->
          <!-- :key is for Vue to keep track of items with ids -->
            <div class="col-sm-4" v-for="product in products" :key="product.id">
              <!-- Bind product to cart -->
              <product  :product="product"
                        @add-to-cart="addToCart(product)"
                        :isInCart="isInCart(product)"
                         />  
            </div><!-- END Product Catalogue -->
          </div>
        </div>

        <!-- Shopping Cart container -->
        <div class="cart">
          <div class="col-md-5 my-5" id="shopping-cart">
            <cart :items="cart"
                  @remove-from-cart="removeFromCart($event)"
                  @pay="pay()" />
          </div>
        </div><!-- END Cart Container -->

      </div><!-- END of App Container -->
    </div><!-- END of Storefront -->
</template>

<script>
import Product from "@/components/Product.vue";
import Cart from "@/components/Cart.vue";
// import Checkout from "@/components/Checkout.vue";

export default {
  name: "app",
  components: {
    Product, 
    Cart, 
    // Checkout
  },
  props: {
    commerce: {
      required: true,
      type: Object
    }
  },
  data() {
    return {
      products: {},
      cart: []
    };
  },

  //When Vue app is created, run these functions to fetch data from API
  created() {
    //List all products from store 
    this.commerce.products.list()
      .then((resp) => {
        //Successful response
        this.products = resp.data;
      })
      //Error
      .catch((error) => {
          alert(error);
      });

      // invoke commerce cart method to retrieve cart in session
      this.commerce.cart.retrieve((cart) => {
        if (!cart.error) {
          this.cart = cart
        }
      });
  },
  //Declare action methods on object
  methods: {

    //Add products to cart
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
    // pay(){
    //   this.cart = [];
    // },
  },
  computed: {
    cartCount(){
      return {
        count: this.count, 
        ...this.cart
      }
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


.cart{
  display: flex;
  justify-content: space-between;
}

</style>