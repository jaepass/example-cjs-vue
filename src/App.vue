<template>
  <div class="storefront">
    
  <!-- Hero component contains header -->
  <store-hero></store-hero>

    <div class="container mx-auto px-4">
      <div class="flex mb-4">
        <div class="row" v-for="category in categories" :key="category">
          <p>{{ category.name }}</p>
          </div>
        </div>
      </div>
      
    <store-footer></store-footer>
    </div>
</template>


<script>
import Commerce from '@chec.io/commerce';
import Hero from "@/components/Hero.vue";
import Footer from "@/components/Footer.vue";

// Initialize store with public key, store key in variable myStore
const myStore = new Commerce('pk_17054571618e73520760e522b00e08ee196503b14e95c', true);

export default {
  name: "app",
  components: {
    'store-hero': Hero,
    'store-footer': Footer,
  },
  data() {
    return {
      categories:[]
    };
  },

  mounted() {
    //List all products from chec 
    myStore.categories.list()
      .then((resp) => {
        //console.log(resp);
        this.categories = resp.data
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
  }
};
</script>

<style>
body {
  background-color: #ffffff;
  font-family: 'Lato', sans-serif;
}

h1, h2, h3, h4{
  text-transform: uppercase;
}

p, a{
  letter-spacing: 2.5px;
}

</style>