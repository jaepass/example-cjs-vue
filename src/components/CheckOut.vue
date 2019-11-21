<template>
  
</template>

<script>
import Commerce from '@chec.io/commerce';

// Initialize store with public key, store key in variable myStore
const myStore = new Commerce('pk_17054571618e73520760e522b00e08ee196503b14e95c', true);

export default {

  mounted() {
    //Generate token checkout
    myStore.checkout.generateToken()
        .then((response) => {
            const checkoutTokenId = response.id; // e.g. chkt_959gvxcZ6lnJ7
            // Grab your order confirmation data from `response` and show your customer something nice!
        })
        .catch((error) => {
                alert(error);
        });  
  },


}

</script>

<style>

</style>