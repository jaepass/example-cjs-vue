# Create a single page product catalogue with Commerce.js and Vue.js

![Demo Image](demo-img.png)

### Visit Live Site
https://jaepass.github.io/example-cjs-vue/

For this guide, we will be creating a single page product display of a Chec storefront using [Commerce.js](https://commercejs.com/) SDK and [Vue.js](https://vuejs.org/) as a framework. 

What is **Commerce.js** you might ask? If this is your first foray into a **headless eCommerce** project, please continue to read on! Another question might then be "What is headless eCommerce?" There are definitely a lot of sources out there explaining what exactly this "headless" concept means. A headless platform has its frontend decoupled so that the data orchestration or inventory management is handled in the backend and fetched using an **API**. This concept completely eliminates the complexity and gives frontend developers the power to easily create an eCommerce web store, an otherwise daunting task if you are a newcomer. When I first started my dev career at [Commerce.js](https://commercejs.com/), I did my fair share of digging and wrote up a [TL;DR](https://dev.to/jaepass/what-is-headless-ecommerce-3nfb).

Commerce.js is an **API-first** eCommerce solution platform aimed at creating seamless eCommerce solutions that easily integrate with any modern tool. As this was my first foray into creating a headless eCommerce solution, being able to jump right in and spit out a **SPA** (Single Page App) web store really establishes [Commerce.js](https://commercejs.com/docs/getting-started) as a powerful developer tool with a low barrier to entry. But I would say the one best selling point about using a headless eCommerce tool like Commerce.js is the complete control you have over your frontend. Think of designing a unique digital experience with customized content consumption all the way through to your purchase flow. No *out-of-the-box* design here. If you can dream it, you can build it with Commerce.js! Please read more into Chec Platform (our API platform) and our Commerce.js SDK [here](commercejs.com/docs).

## Prerequisites

This project assumes you have some knowledge of the below concepts before starting: 

- Some basic knowledge of JavaScript
- Some knowledge of a JS framework like Vue.js
- An idea of the JAMstack architecture and how APIs work

## What you will need to start this project

* IDE Code Editor
* NodeJS, at least v8/10
* npm or yarn

## Some things note

- The goal of this tutorial is to walk you through creating a simple storefront displaying your product catalogue with Commerce.js and Vue.js. This particular project on the repository contains the full checkout process but for the sake of simplicity and easing into using Commerce.js, we will only be focusing our efforts in creating the product display. 

- The styling of this project is done mainly using CSS and a bit of Bootstrap for basic layout. We will not be going into styling details and instead hone our focus in on the logic of Commerce.js.

- If you would like to jump right into forking this repo and customize the storefront as you please, then disregard the rest of this tutorial! Otherwise, let's get right into it!

## Getting started

### 1. Sign up for your Chec account

  - To start building your eCommerce storefront, we first need to get you up and running with a [Chec](https://dashboard.chec.io/signup) account.

  - Did you know you can get started with Chec for **_free_**? Yes, you heard right. Getting set up with our standard merchant account is completely **FREE**! So what are you waiting for? Let's head over to [Chec](https://dashboard.chec.io/signup) to create your account and get rockin' with building your eCommerce website. 

### 2. Upload your products

  - In order to build an eCommerce website, you'd need some data to work with like products and product dtails. So once you've set up your account, let's log in and start [uploading our products](https://dashboard.chec.io/products)! 

  - To keep a visually modular product display, we will be uploading 9 products in total, each with the below details at the bare minimum:
    - Product Image
    - Product Name
    - Price
    - Product Description

## Project setup

For this particular demo storefront integration, we are using [Vue.js](https://vuejs.org/) framework. We're big fans of Vue.js here at Chec Platform/Commerce.js. There are several reasons why: If you love frameworks that are modular, lightweight, performant, and comes packed with the coolest cats like [directives](https://vuejs.org/v2/guide/syntax.html#Directives), you'll love [Vue.js](https://vuejs.org/v2/guide/). 

### 1. Install Vuejs
  - Open your Terminal window and install Vue globally:

  ```
  npm install -g @vue/cli
  ```

### 2. Set up your Vue project:
  **1. To create a new project, run:**

  ```
  vue create your-project-name
  ```

  Follow the next steps to add the following to your project (feel free to opt out for now as you can always install these dependencies separately later on):

- Babel
- CSS Pre-processors: SASS/SCSS (if you plan to use SASS)
- Linter

**2. Change directory into your project folder:**
```
cd your-project-name
```

**3. Install dependencies required by the template (maybe brew yourself a nice cup of coffee after running installation):**
```
npm install
```

**4. Start your local http server and run development:**
```
npm run serve
```

### 3. Inject the Commerce.js logic layer
In order to communicate with the Chec API and fetch data from the backend, we need to install the Commerce.js SDK:
  ```
  npm install @chec/commerce.js
  ```

Now we need to link up our Chec store to our project. To do so, we need to create a new Commerce instance and pass in our public API key (grab your public key from your [Chec dashboard](https://dashboard.chec.io/setup/developer)). Let's open up our `src/main.js` file:

  ```javascript
  //main.js

  // Import Commerce.js as a dependency
  import Commerce from '@chec/commerce.js';

  // Initialize store with public key and store key in variable
  // Commerce also accepts a second argument 'true', enabling the Commerce.js console debugger
  const commerce = new Commerce('ENTER YOUR PUBLIC KEY HERE', true);
  ```

### 4. Instantiating your Chec store

This is where the real fun part starts. You will now see how truly progressive and powerful building a JAMstack project is. All the abstraction of server-side processes is completely decoupled. All you need to do is make requests to various [Chec API endpoints](https://commercejs.com/docs/api/), receive successful responses, then you have your raw data to output beautifully onto your web store. 

> All of our APIs are designed to work either alone or with each other. Our APIs are organized around REST and are designed to have predictable, resource-oriented URLs that use appropriate HTTP response codes to indicate the results of API responses. All of the API responses are JSON encoded.

Still working from our `main.js` file, copy the rest of the code below:

```javascript
//main.js

// Import Commerce.js as a dependency
import Commerce from '@chec/commerce.js';

import Vue from 'vue'
import App from './App.vue'

// Initialize store with public key, store key in variable
const commerce = new Commerce('ENTER YOUR PUBLIC KEY HERE', true);

Vue.config.productionTip = false

// Create a Vue instance
// Pass our Commerce instance as a prop
new Vue({
  render: h => h(App,
    { props: { commerce } }),
}).$mount('#app')
```

Our new Vue instance must be declared as an entry component in our `main.js`. We then have to define our `$mount` property to point to the DOM and tell Vue where the entry component should be mounted. 

### 5. Start creating your product display

We will be coding most of the logic in the `App.vue` file. So let's open up the file and see what we're working with!

If you're starting your project from scratch, the Vue app has neatly laid out the file components for you. For modularity, your HTML markup, JS, and CSS can all live in a single `.vue` extended file. A scaffolded `App.vue` file contains these elements:

- `<template></template>` Within the template tags is where you will be writing your markup for your product display container
- `<script></script>` In the script tags is where the logic of the app will live
- `<style></style>` The style tags is where you'll be styling the components of your app

Or simply start a new file skeleton structure by typing `/` + `tab` key. You will end up with a file structure like this:

```javascript
<template>
  
</template>

<script>
export default {

}
</script>

<style>

</style>
```

Once you have your App.vue skeleton, let's start adding in the elements.

  **1. Add logic in `<script>`**
```javascript
//App.vue

<script>
import Product from "@/components/Product.vue";

export default {
  name: "app",
  components: {
    Product, 
  },
  // Pass commerce as a prop
  props: {
    commerce: {
      required: true,
      type: Object
    }
  },
  // Return our product data 
  data() {
    return {
      products: [],
    };
  },

  //When Vue app is created, run these functions to fetch data from API
  created() {
    //Make a request to list products
    this.commerce.products.list().then((resp) => {
        //Respond with products data upon a successful request
        this.products = resp.data;
    })
    //Handle Error
    .catch((error) => {
        alert(error);
    });
  },
};

</script>
```
Let's start by breaking the above code down in chunks shall we?

In our components property, we need to define `Product` as a **prop** to later return it in our `data()` function below it. The returned object properties (our `Product` in this case) can then be bound to the template view. A **custom directive** which we will later bind to our template is essentially a **prop**, and our prop value is each individual looped product item. (more on this in the next section).

When our App is created, we use Commerce.js `commerce.products.list()` method to respond with a list of our static product objects. As you can see, we are only making a request to our Chec store backend once our app is `created()`. Upon a successful request, we then list out our products, otherwise we respond with an error message. Commerce.js allows us to make asynchronous promise-based calls to only execute our products list, if and when our request was made successfully.

  **2. Add markup in `<template>`**

```html
<!-- App.vue -->

<template>
    <div>
        <!-- Products catalogue -->
        <div class="container mx-auto px-4">
            <div class="flex mb-4">
                <div class="row">
                    <!-- Loop through products and output -->
                    <!-- :key is for Vue to keep track of items -->
                    <div class="col-sm-4" v-for="product in products" :key="product.id">
                        <!-- Bind product to cart -->
                        <product  :product="product"/>  
                        </div><!-- END Product Catalogue -->
                    </div>
                </div>
            </div><!-- END of App Container -->
    </div><!-- END of Storefront -->
</template>
```

Now let's have a look at our template code.

We can safely ignore those class attributes such as `container`, `mx`, `px`, `flex`, `col`, etc. as those are Bootstrap pre-defined class names. These Bootstrap components help to lay out the product display in responsive columns. 

The neat thing about Vue is that it is a declarative framework, meaning we can render dynamic data to the DOM using Vue's straightforward template syntax. Vue also comes packed with built-in directives like `v-for`, which is most fitting to use for looping through our product data here:

```html
<div v-for="product in products" :key="product.id">
```

The v-for directive here helps to loop through each product data object to render. The `:key` attribute gives each looped item a unique condition, which in this case we use our `product.id`. If you're curious in understanding more about the `:key` attribute, the Vue official docs provides more info [here](https://vuejs.org/v2/api/#key).


Nested within is our `<product>` component:
```
<product :product="product" />  
```

We bind our element attributes `v-bind:product="product"` with the `v:bind` directive. `:product="product"` is a shorthand of `v-bind:product`. We will get to creating our Product component in the next section. At this point, what you need to understand is the `<product>` component within the template is what is injecting in and displaying what our products layout. 

Let's now add our Product component: Create a new file in `src/components` and name it `Product.vue`

**1. Add logic in `<script>`**

```javascript
//Product.vue

<script>
export default{
    name: 'product',
    props: ['product']
}
</script>
```

Here we are naming our component and passing our product as props. 

  **2. Add layout in `<template>`**

```html
<template>
    <div class="card my-5 border-0" style="height:41rem;">
        <div class="card-body">
            <img :src="product.media.source" :alt="product.name" class="card-img-top"/>
            <h4 class="title text-center card-title display-5 pt-4">{{product.name}}</h4>
            <p class="description text-center card-text display-5" v-html="product.description"></p>
            <p class="text-center text-muted card-subtitle display-5 price">{{product.price.formatted_with_symbol}}</p>
        </div>
    </div><!-- End of card content -->
</template>
```

The **Commerce.js SDK** is what is allowing us to easily render our product data attributes such as `product.media.source`, `product.name`, `product.price.formatted_with_symbol`. Our Chec data can be rendered using either intepolation with double curly braces or custom directive attributes. Chec's API is beautifully designed with various endpoints to let you as a developer have access to work with all this data. It is now your turn to output your product data onto a unique customized eCommerce web app!
