<template>
    <div class="cart-wrapper">
      <ul class="list-group">
        <div v-if="items.length >= 1"><h3 class="pb-3">Shopping Cart</h3></div>
        <li class=" item-name" v-for="item in items" :key="item.id">
          {{ item.name }} <span class="text-center">{{ item.price.formatted_with_symbol }}</span>
          <button @click="$emit('remove-from-cart', item.id)"
                  class="btn-remove py-2 px-4 float-right">Remove</button>
        </li>
      </ul>
      <div class="total" v-if="items.length >= 1">
        <p class="text-right">Total Due: <b>${{ cartTotal.toFixed(2) }}</b></p>
      </div>

    <button
      v-if="items.length >= 1"
      @click="$emit('generate-checkout')"
      class="btn-checkout form-control mt-3"
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

.cart-wrapper {
  width: 380px;
  padding: 20px;
  box-shadow: 0 0 10px rgb(223, 223, 223);
}

.cart-wrapper h2{
  padding-bottom: 15px;
}

.cart-wrapper ul {
  border: none;
  
}

.cart-wrapper li {
  border-bottom: 1px solid rgba(128, 128, 128, 0.331);
  list-style: none;
  margin-bottom: 15px;
  display: flex;
  justify-content: space-between;
}

.btn-remove {
  border: 1px solid #040034;
  font-size: 12px;
  text-transform: uppercase;
  margin-bottom: 15px;
  transition: all 0.2s ease-in-out;
  cursor: pointer;
}

  .btn-remove:hover{
      background-color: #040034;
      color: white;
  }

.btn-checkout {
    background-color: #040034;
    color: white;
    letter-spacing: 2.75px;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: 500;
    line-height: 25px;
    cursor: pointer;
    transition: all 0.2s ease-in-out;
}

.btn-checkout:hover {
  background-color: black;
}

</style>

