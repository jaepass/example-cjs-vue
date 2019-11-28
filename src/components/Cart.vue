<template>
    <div class="cart-wrapper">
      <ul class="list-group">
        <div v-if="items.length >= 1"><h3 class="pb-3">Shopping Cart</h3></div>
        <li class="list-group-item item-name" v-for="item in items" :key="item.id">
          {{ item.name }} <span class="text-center">{{ item.price.formatted_with_symbol }}</span>
          <button @click="$emit('remove-from-cart', item.id)"
                  class="bg-transparent py-2 px-4 border hover:border-transparent rounded float-right">Remove</button>
                  
        </li>
      </ul>
      <div class="card" v-if="items.length >= 1">
        <h4 class="text-center">Total Due: ${{ cartTotal.toFixed(2) }}</h4>
      </div>

    <button
      v-if="items.length >= 1"
      @click="$emit('generate-checkout')"
      class="checkout-btn form-control"
    >Checkout</button>
  </div>
</template>

<script>
export default {
    props: ["items"],
    computed: {
      cartTotal() {
          return this.items.reduce((acc, item) => acc + Number(item.price.formatted), 0);
      },
    },
};
</script>

<style>
.cart-wrapper h2{
  padding-bottom: 15px;
}

.checkout-btn{
    background-color: black;
    color: white;
    letter-spacing: 2.75px;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: 500;
}

</style>

