<template>
    <div class="checkout-wrapper">
        <form v-if="checkout">
            <label>Customer Information
                <input type="text" id="name" name="Name" placeholder="Name" v-model="checkoutData.customer.name" required>
            </label>
        </form>
    </div>
  
</template>

<script>
// import Commerce from '@chec.io/commerce';


export default {

    data(){
        return
    }

 


}

</script>

<style>

</style>