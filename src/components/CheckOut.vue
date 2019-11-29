<template>
    <div class="checkout-wrapper">
        <h3>Checkout</h3>
        <form>
            <h4 class="mt-4 pt-3 border-top">Customer Information</h4>

                <label class="d-block pt-3" for="firstName">First Name</label>
                <input class="p-1 col-xs-3" type="text" v-model="customerData.personal.firstName" name="firstName" placeholder="Enter your first name" required />

                <label class="d-block pt-3" for="lastName">Last Name</label>
                <input class="p-1 col-xs-3" type="text" v-model="customerData.personal.lastName" name="lastName" placeholder="Enter your last name" required />

                 <label class="d-block pt-3" for="lastName">Email</label>
                <input class="p-1 form-control" type="text" v-model="customerData.personal.email" name="email" placeholder="Enter your email" required />

            <h4 class="mt-5 pt-3 border-top">Shipping Details</h4>

                <label class="d-block pt-3" for="streetAddress">Street Address</label>
                <input class="p-1 form-control" type="text" v-model="customerData.shipping.streetAddress" name="shipping[street-address]" placeholder="Enter your street address" required />

                <label class="d-block pt-3" for="city">City</label>
                <input class="p-1 form-control" type="text" v-model="customerData.shipping.city" name="shipping[city]" placeholder="Enter your city" required />

                <label class="d-block pt-3" for="city">Postal Code/Zip Code</label>
                <input class="p-1 form-control" type="text" v-model="customerData.shipping.postalZip" name="shipping[postal-zip]" placeholder="Enter your postal or zip code" required />

                <label class="d-block pt-3" for="city">Country</label>
                <input class="p-1 form-control" type="text" v-model="customerData.shipping.country" name="shipping[country]" placeholder="Enter your country" required />

                <label class="d-block pt-3" for="city">Shipping Option</label>


                <select v-model="shippingOption" name="shippingOption" class="p-1">
                <option value="" disabled>Select a shipping method</option>
                <option v-for="option of shippingOptions" :value="option.id" :key="option.id">{{ `${option.description} - $${option.price.formatted_with_code}` }}</option>
            </select>

            <h4 class="mt-5 pt-3 border-top">Payment Information</h4>

                <label class="d-block pt-3" for="cardNum">Credit Card Number</label>
                <input class="p-1 form-control" type="text" name="payment[card-num]" v-model="customerData.payment.cardNum" placeholder="Enter your card number" />

                <label class="d-block pt-3" for="expMonth">Expiry Month</label>
                <input class="p-1 col-xs-3" type="text" name="payment[exp-month]" v-model="customerData.payment.expMonth" placeholder="Card expiry month" />

                <label class="d-block pt-3" for="expYear">Expiry Year</label>
                <input class="p-1 col-xs-3" type="text" name="payment[exp-year]" v-model="customerData.payment.expYear" placeholder="Card expiry year" />

                <label class="d-block pt-3" for="ccv">CCV</label>
                <input class="p-1 col-xs-3" type="text" name="payment[ccv]" v-model="customerData.payment.ccv" placeholder="CCV (3 digits)" />

            <button class="mt-5 py-2 form-control confirm-btn" @click.prevent="confirmOrder()">Confirm Order</button>
            
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
                    firstName: 'Jane',
                    lastName: 'Doe',
                    email: 'janedoe@email.com',
                },
                shipping: {
                    streetAddress: '123 Main St',
                    city: 'Vancouver',
                    postalZip: 'V1A 2B3',
                    country: 'Canada',
                    shippingOption: '',
                    // shippingOptions: []
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
    methods: {
        confirmOrder () {

            const confirmedOrder = 
                this.customerData.personal;
                this.customerData.shipping;
                this.customerData.payment;
                this.$emit('confirm-order', this.checkout.id, confirmedOrder)
        }
    }
}

</script>

<style>

.confirm-btn{
    background-color: black;
    color: white;
    letter-spacing: 2.8px;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: 500;
}


</style>