<template>
    <div class="hero-wrapper">
            
            <div class="hero-img-1">
                <!-- <div class="logo" href="/">
                    <img width="175px" src="@/assets/logo.png" alt="Tribal Logo">
                </div> -->
            </div>
            
            <nav>
                <div class="nav-items">
                    <a href=""><p class="shop">shop</p></a>
                    <a href="/demostore-cjs/#wishlist"><img width="28px" src="@/assets/fav-icon.svg" alt="wishlist icon"></a>
                    <a href=""><img width="28px" src="@/assets/shopcart-icon.svg" alt="Tribal Logo"></a>
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
}

nav{
    grid-area: nav;
    background: #040034;
    background-size: cover;
    position: relative;
}

.nav-items{
    display: flex;
    justify-content: flex-end;
    position: relative;
    top: 50%;
    transform: translateY(-50%);
    
}

.nav-items a{
    padding-left: 10px;
}

.shop{
    color: white;
    text-transform: uppercase;
    border: 1px solid white;
    padding: 5px 9px;
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



.logo{
    padding: 30px 0 0 30px;
    cursor: pointer;
}

</style>