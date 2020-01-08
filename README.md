# Create a single page product catalogue with Commerce.js and Vue.js

![Demo Image](demo-img.png)

### Visit Live Site
https://jaepass.github.io/example-cjs-vue/

For this guide, we will be creating a single page product display of a Chec storefront using [Commerce.js](https://commercejs.com/) SDK and [Vue.js](https://vuejs.org/) as a framework. 

What is Commerce.js you might ask? If this is your first foray into a Headless eCommerce project, please continue to read on! Another question might then be "What is headless eCommerce?" There are definitely a lot of sources out there explaining what exactly this "headless" concept means. When I first started my dev career at [Commerce.js](https://commercejs.com/), I did my fair share of digging and wrote up a [TL;DR](https://dev.to/jaepass/what-is-headless-ecommerce-3nfb).

So now what is Commerce.js? Commerce.js is an API-first eCommerce solution platform aimed at creating seamless eCommerce solution that easily integrates with any modern tool. As this was my first foray into creating a headless eCommerce solution as a new developer, being able to jump right in an spit out a scaffold of an eCommerce app with Commerce.js really reinstates the power and low barrier entry of this developer tool. Please read more into Chec Platform (our API platform) and our Commerce.js SDK [here](http://support.chec.io/en/articles/513192-what-is-chec-platform-chec-dashboard-and-commerce-js).

## Prerequisites

There are a few basic prerequisites before starting this project. 

- Some basic knowledge of JavaScript
- Some knowledge of a JS framework like Vue.js
- An idea of the concept of JAMstack and how APIs work

## What you will need to start this project

* IDE Code Editor
* NodeJS, at least v8/10
* npm or yarn

## Some things note

The goal of this tutorial is to walk you through creating a simple storefront displaying your product catalogue with Commerce.js and Vue.js. This particular project on the repository contains the full checkout process but for the sake of simplicity and easing into using Commerce.js, we will only be focusing our efforts in creating the product display. 

The styling of this project is done mainly using CSS and a bit of Bootstrap for basic layout. We will not be going into too much details on the styling and instead hone our focus in on the logic of Commerce.js.

If you would like to jump right into forking the repo and customize the storefront as you please, then disregard the rest of this tutorial! Otherwise, let's get right into it!

## Getting started

### 1. Sign up for Chec account
  - To start building your eCommerce storefront, we first need to get you up and running with a [Chec](https://dashboard.chec.io/signup) account.

  - Did you know you can get started with Chec for free? Yes, you heard right. Getting set up with our standard merchant account is completely FREE! So what are you waiting for? Let's head over to [Chec](https://dashboard.chec.io/signup) to create your account and get started with creating your eCommerce website. 

### 2. Upload your products

  - In order to build an eCommerce website, you'd need some data to work with like products and product information. So once you've set up your account, let's log in and start [uploading our products](https://dashboard.chec.io/products)! 

  - To keep a visually modular product display, we will be uploading 9 products in total, each with the below details at bare minimum:
    - Product Image
    - Product Name
    - Price
    - Product Description


## Project setup




```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
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
