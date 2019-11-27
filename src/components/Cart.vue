<template>
    <div class="cart-wrapper">
      <ul class="list-group">
        <div v-if="items.length >= 1"><h2>Shopping Cart</h2></div>
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
      :disabled="items.length === 0"
      @click="$emit('checkout')"
      class="btn btn-info form-control"
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

</style>

