# Create a single page product catalogue with Commerce.js and Vue.js

![Demo Image](demo-img.png)

### Visit Live Site
https://jaepass.github.io/example-cjs-vue/

For this guide, we will be creating a single page product display of a Chec storefront using [Commerce.js](https://commercejs.com/) SDK and [Vue.js](https://vuejs.org/) as a framework. 

What is **Commerce.js** you might ask? If this is your first foray into a **headless eCommerce** project, please continue to read on! Another question might then be "What is headless eCommerce?" There are definitely a lot of sources out there explaining what exactly this "headless" concept means. A headless platform has its frontend decoupled so that the data orchestration or inventory management is handled in the backend and fetched using an API. This concept completely eliminates the complexity and gives frontend developers the power to easily create an eCommerce web store, an otherwise daunting task if you are a newcomer. When I first started my dev career at [Commerce.js](https://commercejs.com/), I did my fair share of digging and wrote up a [TL;DR](https://dev.to/jaepass/what-is-headless-ecommerce-3nfb).

So now what is Commerce.js? Commerce.js is an **API-first** eCommerce solution platform aimed at creating seamless eCommerce solutions that easily integrate with any modern tool. As this was my first foray into creating a headless eCommerce solution, being able to jump right in and spit out a scaffold of an eCommerce app really establishes[Commerce.js](https://commercejs.com/docs/getting-started) as a powerful developer tool with a low barrier to entry. Please read more into Chec Platform (our API platform) and our Commerce.js SDK [here](commercejs.com/docs).

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

- The styling of this project is done mainly using CSS and a bit of Bootstrap for basic layout. We will not be going into too much details on the styling and instead hone our focus in on the logic of Commerce.js.

- If you would like to jump right into forking this repo and customize the storefront as you please, then disregard the rest of this tutorial! Otherwise, let's get right into it!

## Getting started

### 1. Sign up for your Chec account

  - To start building your eCommerce storefront, we first need to get you up and running with a [Chec](https://dashboard.chec.io/signup) account.

  - Did you know you can get started with Chec for **_free_**? Yes, you heard right. Getting set up with our standard merchant account is completely **FREE**! So what are you waiting for? Let's head over to [Chec](https://dashboard.chec.io/signup) to create your account and get rockin' with creating your eCommerce website. 

### 2. Upload your products

  - In order to build an eCommerce website, you'd need some data to work with like products and product information. So once you've set up your account, let's log in and start [uploading our products](https://dashboard.chec.io/products)! 

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
  1. To create a new project, run:

  ```
  vue create your-project-name
  ```

  2. Change directory into your project folder:
  ```
  cd your-project-name
  ```

  3. Install dependencies required by the template (maybe brew yourself a nice cup of coffee after running installation):
  ```
  npm install
  ```

  4. Start your local http server and run development:
  ```
  npm run serve
  ```

### 3. Inject the Commerce.js logic layer
  1. In order to communicate with the Chec API and fetch data from the backend, we need to install the Commerce.js SDK:
  ```
  npm install @chec/commerce.js
  ```

  2. Now we need to link up our Chec store to our project. To do so, we need to create a new Commerce instance and pass in our public API key (grab your public key from your [Chec dashboard](https://dashboard.chec.io/setup/developer)):

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
const commerce = new Commerce('pk_17054571618e73520760e522b00e08ee196503b14e95c', true);

Vue.config.productionTip = false

//Here, we pass our Commerce instance as a prop
new Vue({
  render: h => h(App,
    { props: { commerce } }),
}).$mount('#app')
```

### 5. Start creating your product display

We will be coding most of the logic in the `App.vue` file. So let's open up the file and see what we're working with!

If you're starting your project from scratch, the Vue app has neatly laid out the file components for you. A scaffolded `App.js` file contains these elements:

- `<template></template>` Within the template tags is where you will be laying out the content of your product display
- `<script></script>` In the script tags is where the logic of the app will live
- `<style></style>` The style tags is where you'll be styling the components of your app

Or simply start a new Vue skeleton structure by typing `/` + `tab` key. You will end up with a file structure like this:

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

  1. Add layout in `<template>`

```html
<template>
    <div>
        <!-- Products catalogue -->
        <div class="container mx-auto px-4">
            <div class="flex mb-4">
                <div class="row">
                    <!-- Loop through products and output -->
                    <!-- :key is for Vue to keep track of items with ids -->
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

Now let's break down the code shall we?

We can safely ignore those class attributes such as `container`, `mx`, `px`, `flex`, `col`, etc. as those are Bootstrap pre-defined class names. These Bootstrap components help to lay out the product display in responsive columns. 

Nested within the Bootstrap div tags is a `<product>` component. We will touch more on this below when we get into the `script` component.

Vue is a declarative framework, you can read more into this [here](). We can pass directives like `v-bind:product="product"`

  2. Add logic in `<script>`
```javascript
<script>
import Product from "@/components/Product.vue";

export default {
  name: "app",
  components: {
    Product, 
  },
  props: {
    commerce: {
      required: true,
      type: Object
    }
  },
  data() {
    return {
      products: [],
    };
  },

  //When Vue app is created, run these functions to fetch data from API
  created() {
    //List all products from store 
    this.commerce.products.list().then((resp) => {
        //Successful response
        this.products = resp.data;
    })
    //Error
    .catch((error) => {
        alert(error);
    });
  },
};

</script>
```

Now, let's add a Product component

  1. Add layout in `<template>`

```html
<!-- Products -->
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

2. Add logic in `<script>`

```javascript
<script>
export default{
    name: 'product',
    props: ['product']
}
</script>
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
