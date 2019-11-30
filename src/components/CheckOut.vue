<template>
    <div class="checkout-wrapper">
        <h3>Checkout</h3>
        <form>
            <h4 class="mt-4 pt-3 border-top">Customer Information</h4>

                <label class="d-block pt-3" for="customerFirstName">First Name</label>
                <input class="p-1 col-xs-3" type="text" v-model="customerFirstName" name="customerFirstName" placeholder="Enter your first name" required />

                <label class="d-block pt-3" for="customerLastName">Last Name</label>
                <input class="p-1 col-xs-3" type="text" v-model="customerLastName" name="customerLastName" placeholder="Enter your last name" required />

                 <label class="d-block pt-3" for="customerEmail">Email</label>
                <input class="p-1 form-control" type="text" v-model="customerEmail" name="customerEmail" placeholder="Enter your email" required />

            <h4 class="mt-5 pt-3 border-top">Shipping Details</h4>

                <label class="d-block pt-3" for="street">Full Name</label>
                <input class="p-1 form-control" type="text" v-model="shippingName" name="shippingName" placeholder="Enter your shipping full name" required />

                <label class="d-block pt-3" for="street">Street Address</label>
                <input class="p-1 form-control" type="text" v-model="street" name="street" placeholder="Enter your street address" required />

                <label class="d-block pt-3" for="city">City</label>
                <input class="p-1 form-control" type="text" v-model="city" name="city" placeholder="Enter your city" required />

                <label class="d-block pt-3" for="provinceState">Province/State</label>
                <input class="p-1 form-control" type="text" v-model="provinceState" name="provinceState" placeholder="Select your province/state" required />

                <select v-model="provinceState" name="provinceState" class="">
                <option value="" disabled>Province/State</option>
                <option v-for="(subdivisionName, subdivisionCode, index) of subdivisions" :value="subdivisionCode" :key="index">{{subdivisionName}}</option>
                </select>

                <select v-model="country" name="country" class="db mb2">
                <option value="" disabled>Country</option>
                <option v-for="(countryName, index) of shippingCountries" :value="countryCode" :key="index">{{countryName}}</option>
                </select>
                

                <label class="d-block pt-3" for="city">Shipping Option</label>
                <select v-model="shippingMethod" name="shippingMethod" class="p-1">
                <option value="" disabled>Select a shipping method</option>
                <option v-for="option of shippingOptions" :value="option.id" :key="option.id">{{ `${option.description} - $${option.price.formatted_with_code}` }}</option>
            </select>

            <h4 class="mt-5 pt-3 border-top">Payment Information</h4>

                <label class="d-block pt-3" for="cardNum">Credit Card Number</label>
                <input class="p-1 form-control" type="text" name="cardNum" v-model="cardNum" placeholder="Enter your card number" />

                <label class="d-block pt-3" for="exMonth">Expiry Month</label>
                <input class="p-1 col-xs-3" type="text" name="exMonth" v-model="exMonth" placeholder="Card expiry month" />

                <label class="d-block pt-3" for="exYear">Expiry Year</label>
                <input class="p-1 col-xs-3" type="text" name="exYear" v-model="exYear" placeholder="Card expiry year" />

                <label class="d-block pt-3" for="ccv">CCV</label>
                <input class="p-1 col-xs-3" type="text" name="ccv" v-model="ccv" placeholder="CCV (3 digits)" />

            <button class="mt-5 py-2 form-control confirm-btn" @click.prevent="confirmOrder()">Confirm Order</button>
            
        </form>
    </div>
</template>

<script>

export default {
    name: 'checkout',
    props: ['commerce', 'checkout'],

    created(){
         this.getshippingCountries()
         this.getRegions(this.country)
    },

    data(){
        return{
            //Handle customer input
            customerFirstName: 'Jane',
            customerLastName: 'Doe',
            customerEmail: 'janedoe@email.com',
            //Handle shipping input
            shippingName: 'Jane Doe',
            street: '123 Main St',
            city: 'Vancouver',
            provinceState: '',
            postalZip: 'V1A 2B3',
            country: 'CA',
            //Handle fulfillment input
            shippingMethod: '',
            shippingMethods: [],
            shippingMethodsId: {},
            //Handle payment input
            cardNum: '4242 4242 4242 4242',
            exMonth: '01',
            exYear: '2021',
            ccv: '123',
            billingPostalZip: 'V1A 2B3',
            subdivisions: {},
            shippingCountries: {}
        }
    },
    methods: {

        getShippingCountries(){
            this.commerce.services.localeListShippingCountries(this.checkout.id).then((resp) => 
                //Success
                this.shippingCountries = resp.countries
            )
            .catch((error) => {
                alert(error)
            })
        },

        getRegions(countryCode){
            this.commerce.services.localeListShippingSubdivisions(this.checkout.id, countryCode).then((resp) => 
                //Success
                this.subdivisions = resp.subdivisions
            )
            .catch((error) => {
                alert(error)
            })
        },

        confirmOrder(){
            const confirmedOrder = {
                line_items: this.checkout.live.line_items,
                customer: {
                    firstname: this.customerFirstName,
                    lastname: this.customerLastName,
                    email: this.customerEmail
                },
                shipping: {
                    name: this.shippingName,
                    street: this.street,
                    town_city: this.city,
                    county_state: this.provinceState,
                    postal_zip_code: this.postalZipcode,
                    country: this.country,
                },
                fulfillment: {
                    shipping_method: this.shippingMethod.id
                },
                payment: {
                    gateway: "test_gateway",
                    card: {
                        number: this.cardNum,
                        expiry_month: this.exMonth,
                        expiry_year: this.exYear,
                        cvc: this.ccv,
                        postal_zip_code: this.billingPostalZip
                    }
                }
            };
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