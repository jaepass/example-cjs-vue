<!-- Template for Wishlist Modal  -->

<!-- Custom event handler $emit on child component
to send data back to parent component
-->
<template>
  <div class="wishlist-wrapper">
    <ul class="list-group">
      <div v-if="items.length >= 1"><h2>Wishlist</h2></div>
      <li class="list-group-item item-name" v-for="item in items" :key="item.id">
        {{ item.name }} <span class="text-center">{{ item.price.formatted_with_symbol }}</span>
        <button
          @click="$emit('remove-from-wishlist',item)"
          class="bg-transparent py-2 px-4 border hover:border-transparent rounded float-right"
        >Remove</button>
      </li>
    </ul>
    
  </div>
</template>
<script>
export default {
  props: ["items"]
  
};
</script>

<style>
  .wishlist-wrapper h2{
    padding-bottom: 15px;
  }

  .item-name{
    font-weight: 700;
  }

  span{
    color: grey;
    font-weight: 300;
  }

  button{
    cursor: pointer;
    transition: all 0.3s ease-in-out;
  }

    button:hover{
    cursor: pointer;
    font-weight: 700;
  }
</style>