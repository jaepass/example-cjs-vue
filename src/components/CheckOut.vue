<template>
    <div class="checkout-wrapper">
        <h3>Checkout</h3>
        <form>
            <h4>Customer Information</h4>

                <label for="firstName">First Name</label>
                <input type="text" v-model="firstName" name="firstName" placeholder="Enter your first name" required />

                <label for="lastName">Last Name</label>
                <input type="text" v-model="lasttName" name="lastName" placeholder="Enter your last name" required />

                 <label for="lastName">Email</label>
                <input type="text" v-model="email" name="email" placeholder="Enter your email" required />

            <h2>Shipping Details</h2>

                <label for="streetAddress">Street Address</label>
                <input type="text" v-model="streetAddress" name="streetAddress" placeholder="Enter your street address" required />

                <label for="city">City</label>
                <input type="text" v-model="city" name="city" placeholder="Enter your city" required />

                <label for="city">Postal Code/Zip Code</label>
                <input type="text" v-model="postalZip" name="postalZip" placeholder="Enter your postal or zip code" required />

            <button class="btn btn-primary" @click.prevent="confirmOrder()">Confirm Order</button>
            
        </form>
    </div>
  
</template>

<script>

export default {
    name: 'checkout',
    props: ['commerce', 'checkout'],

    data(){
        return{
            firstName: '',
            lastName: '',
            email: '',
            streetAddress: '',
            city: '',
            postalZip: '',
            country: 'Canada',
            cardNumber: '4242 4242 4242 4242',
            expMonth: '01',
            expYear: '2021',
            ccv: '123',
            billingPostalZipcode: '32825',
            countries: {},
        }
    },
    
 


}

</script>

<style>

</style>