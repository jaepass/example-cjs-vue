# Create a single page product catalogue with Commerce.js and Vue.js

![Demo Image](demo-img.png)

### Visit Live Site
https://jaepass.github.io/example-cjs-vue/

For this guide, we will be creating a single page product display of a Chec storefront using [Commerce.js](https://commercejs.com/) SDK and [Vue.js](https://vuejs.org/) as a framework. 

What is **Commerce.js** you might ask? If this is your first foray into a **headless eCommerce** project, please continue to read on! Another question might then be "What is headless eCommerce?" There are definitely a lot of sources out there explaining what exactly this "headless" concept means. A headless platform has its frontend decoupled so that the data orchestration or inventory management is handled in the backend and fetched using an API. This concept completely eliminates the complexity and gives frontend developers the power to easily create an eCommerce web store, an otherwise daunting task if you are a newcomer. When I first started my dev career at [Commerce.js](https://commercejs.com/), I did my fair share of digging and wrote up a [TL;DR](https://dev.to/jaepass/what-is-headless-ecommerce-3nfb).

So now what is Commerce.js? Commerce.js is an **API-first** eCommerce solution platform aimed at creating seamless eCommerce solutions that easily integrate with any modern tool. As this was my first foray into creating a headless eCommerce solution, being able to jump right in and spit out a scaffold of an eCommerce app with Commerce.js really reinstates the power and low barrier entry of the [Commerce.js SDK](https://commercejs.com/docs/getting-started) developer tool. Please read more into Chec Platform (our API platform) and our Commerce.js SDK [here](commercejs.com/docs).

## Prerequisites

We are assuming you have some knowledge of the below concepts before starting this project: 

- Some basic knowledge of JavaScript
- Some knowledge of a JS framework like Vue.js
- An idea of the concept of JAMstack and how APIs work

## What you will need to start this project

* IDE Code Editor
* NodeJS, at least v8/10
* npm or yarn

## Some things note

- The goal of this tutorial is to walk you through creating a simple storefront displaying your product catalogue with Commerce.js and Vue.js. This particular project on the repository contains the full checkout process but for the sake of simplicity and easing into using Commerce.js, we will only be focusing our efforts in creating the product display. 

- The styling of this project is done mainly using CSS and a bit of Bootstrap for basic layout. We will not be going into too much details on the styling and instead hone our focus in on the logic of Commerce.js.

- If you would like to jump right into forking the repo and customize the storefront as you please, then disregard the rest of this tutorial! Otherwise, let's get right into it!

## Getting started

### 1. Sign up for your Chec account

  - To start building your eCommerce storefront, we first need to get you up and running with a [Chec](https://dashboard.chec.io/signup) account.

  - Did you know you can get started with Chec for free? Yes, you heard right. Getting set up with our standard merchant account is completely FREE! So what are you waiting for? Let's head over to [Chec](https://dashboard.chec.io/signup) to create your account and get going with creating your eCommerce website. 

### 2. Upload your products

  - In order to build an eCommerce website, you'd need some data to work with like products and product information. So once you've set up your account, let's log in and start [uploading our products](https://dashboard.chec.io/products)! 

  - To keep a visually modular product display, we will be uploading 9 products in total, each with the below details at the bare minimum:
    - Product Image
    - Product Name
    - Price
    - Product Description

## Project setup

For this particular demo storefront integration, we are using [Vue.js](https://vuejs.org/) framework. We're big fans of Vue.js here at Chec Platform/Commerce.js. There are several reasons why: If you love frameworks that are modular, performant, and comes packed with the coolest cats like [directives](https://vuejs.org/v2/guide/syntax.html#Directives), you'll love [Vue.js](https://vuejs.org/v2/guide/). 

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

  3. Install dependencies required by the template (maybe brew yourself a nice cup of coffee while you wait):
  ```
  npm install
  ```

  4. Start your local http server and run development:
  ```
  npm run serve
  ```

### Inject the Commerce.js logic layer
  1. In order to communicate with the Chec API and fetch data from the backend, we need to install the Commerce.js SDK:
  ```
  npm install @chec/commerce.js
  ```

  2. Now we need to link up our Chec store to our project. To do so, we need to create a new Commerce instance and pass in our public API key (grab your public key from your [Chec dashboard](https://dashboard.chec.io/setup/developer):

  ```
  //main.js

  // Import Commerce.js as a dependency
  import Commerce from '@chec/commerce.js';

  // Initialize store with public key and store key in variable
  const commerce = new Commerce('pk_17054571618e73520760e522b00e08ee196503b14e95c', true);
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
