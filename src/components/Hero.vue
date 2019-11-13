<template>
    <div class="hero-wrapper">
            
            <div class="hero-img-1">
                <div class="logo" href="/">
                    <img width="175px" src="@/assets/logo.png" alt="Tribal Logo">
                </div>
                <div class="hero-text">
                     <a href="/demostore-vue2/#shop"><p class="discover">discover</p></a>
                     <p>classic timepieces</p>
                </div>
            </div>
            
            <nav>
                <div class="nav-items">
                    <a href="/demostore-vue2/#shop"><p class="shop">shop</p></a>
                    <a href="/demostore-vue2/#wishlist"><img width="28px" src="@/assets/fav-icon.svg" alt="wishlist icon"></a>
                    <a href="/demostore-vue2/#shopping-cart"><img width="28px" src="@/assets/shopcart-icon.svg" alt="Tribal Logo"></a>
                </div>
            </nav>

            <div class="hero-img-2">
            </div>

            <div class="hero-img-3">
            </div>
       
    </div>
</template>


<script>


   export default{

   }
</script>

<style>

.hero-wrapper {
    display: grid;
    grid-template-areas: 
        "img1   nav"
        "img1   img2"
        "img1   img3";
	grid-template-rows: 80px 1fr 1fr;
	grid-template-columns: 55% auto;
    grid-gap: 10px;
    height: 100vh;
}

.hero-img-1{
    background-image: url("../assets/hero-img.jpg");
    grid-area: img1;
    background-repeat: no-repeat;
    background-size: cover;
    position: relative;
}

.logo{
    padding: 30px 0 0 30px;
    cursor: pointer;
}

.logo img{
    width: 120px;
}

.hero-text{
    position: absolute;
    top: 60%;
    left: 50%;
    transform: translateX(-50%);
    text-align: center;
}

.hero-text a{
    text-decoration: none;
}

.hero-text p{
     color: white;
     text-transform: uppercase;
}

.discover{
    color: white;
    text-transform: uppercase;
    border: 1.5px solid white;
    padding: 9px 20px;
    margin-bottom: 20px;
    transition: all 0.3s ease-in-out;
}

.discover:hover{
    color: #040034;
    background-color: #fff;
}


nav{
    grid-area: nav;
    background: #040034;
    background-size: cover;
    /* position: relative; */
    position: sticky;
}

.nav-items{
    display: flex;
    justify-content: flex-end;
    position: relative;
    padding-top: 10px;
    padding-right: 20px;
    top: 50%;
    transform: translateY(-50%);
    
}

.nav-items a{
    padding-left: 20px;
    text-decoration: none;
}

.shop{
    color: white;
    text-transform: uppercase;
    border: 1px solid white;
    padding: 5px 20px;
    margin: 0;
    transition: all 0.3s ease-in-out;
}

.shop:hover{
    color: #040034;
    background-color: #fff;
}

.hero-img-2{
    background-image: url("../assets/hero-img2.jpg");
    grid-area: img2;
    background-repeat: no-repeat;
    background-size: cover;
    object-fit: contain;
}

.hero-img-3{
    background-image: url("../assets/hero-img3.jpg");
    grid-area: img3;
    background-repeat: no-repeat;
    background-size: cover;
    object-fit: contain;
}



</style>