<template>
    <div class="hero-wrapper">
        <header>
            
            <div class="logo" href="/">
                <img width="175px" src="@/assets/logo.png" alt="Tribal Logo">
            </div>
            
            <nav class="ml-auto">
                <a href="/demostore-cjs/#wishlist"><img width="28px" src="@/assets/fav-icon.svg" alt="wishlist icon"></a>
                <a href=""><img width="28px" src="@/assets/shopcart-icon.svg" alt="Tribal Logo"></a>
            </nav>
            <div class="hero-bg"></div>
        </header>

            <img width="675px" src="@/assets/hero-img.jpg" class="hero-img" alt="hero image">

            <div class="hero-text">
                <h1>Street</h1>
                <h1>Runway</h1>
                <h1>Chic</h1>
            </div>

        <div class="shop-scroll">
            <h3>shop</h3>
            <div class="shop-line"></div>
        </div>

    </div>
</template>


<script>
   export default{

   }
</script>

<style>

.hero-wrapper {
    position: relative;
    margin-bottom: 200px;
}

header{
    display: flex;
    z-index: 999;
}

nav{
    z-index: 999;
    padding: 30px 30px 0 0;
    position: fixed;
    right: 0;
}

nav a img {
    margin-left: 25px;
}

.logo{
    padding: 30px 0 0 30px;
    cursor: pointer;
}

.hero-img{
    position: relative;
    z-index: 1;
    display: flex;
    left: 50%;
    top: 50%;
    transform: translateX(-50%);
}


.hero-bg {
    position: absolute;
    height: 80vh;
    width: 50vw;
    background-color: #DBA28B;
    display: flex;
    right: 0;
}

.hero-text{
    position: absolute;
    top: 60%;
    left: 135px;
    transform: translateY(-50%);
    z-index: 999;
    padding: 20px 20px 20px 30px;
    background-color: black;
}

.hero-text h1{
    color: white;
    font-weight: 700;
    font-size: 45px;
    letter-spacing: 25px;
    line-height: 90px;
}


.hero-text h1 span{
    color: white;
}

.shop-scroll{
    position: absolute;
    transform: translateY(-50%);
    z-index: 999;
    right: 100px;
    display: flex;
}

.shop-scroll h3{
    font-weight: 700;
    letter-spacing: 22px;
    bottom: 10px;
    padding-top: 20px;
    padding-right: 10px;
}

.shop-line{
    height:120px;
    border: 1px solid black;
    display: flex; 
    bottom: -20px;
    position: relative;
}


@media only screen and (max-width: 400px){

    nav{
        padding-top: 20px;
    }

    .hero-wrapper {
        margin-bottom: 420px;
    }

    .hero-img{
        width: 325px;
        padding-top: 20px;
    }

    .hero-text{
        position: absolute;
        top: 68vh;
        left: 25px;
        padding: 20px 20px 20px 30px; 
    }

    .hero-text h1{
        font-size: 25px;
        letter-spacing: 18px;
        line-height: 60px;
    }

    .logo {
        padding-top: 20px;
    }

    .logo img {
        width: 125px;
    }

    .shop-scroll{
        top: 90vh;
        right: 100px;
    }

    .shop-scroll h3{
        font-size: 20px;
        letter-spacing: 18px;
    }

    .shop-line{
        height:80px;
    }
}

</style>