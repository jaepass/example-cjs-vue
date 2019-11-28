<template>
    <div class="checkout-wrapper">
        <h3>Checkout</h3>
        <form>
            <h4>Customer Information</h4>

                <label for="firstName">First Name</label>
                <input type="text" v-model="customerData.personal.firstName" name="firstName" placeholder="Enter your first name" required />

                <label for="lastName">Last Name</label>
                <input type="text" v-model="customerData.personal.lastName" name="lastName" placeholder="Enter your last name" required />

                 <label for="lastName">Email</label>
                <input type="text" v-model="customerData.personal.email" name="email" placeholder="Enter your email" required />

            <h4>Shipping Details</h4>

                <label for="streetAddress">Street Address</label>
                <input type="text" v-model="customerData.shipping.streetAddress" name="shipping[street-address]" placeholder="Enter your street address" required />

                <label for="city">City</label>
                <input type="text" v-model="customerData.shipping.city" name="shipping[city]" placeholder="Enter your city" required />

                <label for="city">Postal Code/Zip Code</label>
                <input type="text" v-model="customerData.shipping.postalZip" name="shipping[postal-zip]" placeholder="Enter your postal or zip code" required />

                <label for="city">Country</label>
                <input type="text" v-model="customerData.shipping.country" name="shipping[country]" placeholder="Enter your country" required />

            <h4>Payment Information</h4>

                <label for="cardNum">Credit Card Number</label>
                <input type="text" name="payment[card-num]" v-model="customerData.payment.cardNum" placeholder="Enter your card number" />

                <label for="expMonth">Expiry Month</label>
                <input type="text" name="payment[exp-month]" v-model="customerData.payment.expMonth" placeholder="Card expiry month" />

                <label for="expYear">Expiry Year</label>
                <input type="text" name="payment[exp-year]" v-model="customerData.payment.expYear" placeholder="Card expiry year" />

                <label for="ccv">CCV</label>
                <input type="text" name="payment[ccv]" v-model="customerData.payment.ccv" placeholder="CCV (3 digits)" />

            <button class="btn btn-info form-control" @click.prevent="confirmOrder()">Confirm Order</button>
            
        </form>
    </div>
  
</template>

<script>

export default {
    name: 'checkout',
    props: ['commerce', 'checkout'],

    data(){
        return{
            customerData: {
                personal: {
                    firstName: '',
                    lastName: '',
                    email: '',
                },
                shipping: {
                    streetAddress: '',
                    city: '',
                    postalZip: '',
                    country: 'Canada',
                },
                payment: {
                    cardNum: '4242 4242 4242 4242',
                    expMonth: '01',
                    expYear: '2021',
                    ccv: '123',
                }
            }
        }
    },
    
 


}

</script>

<style>

</style>