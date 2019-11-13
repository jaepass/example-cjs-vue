<!-- Products in wishlist -->
<template>
    <div class="card my-5" style="height:41rem;">
        <div class="card-body">
            <img :src="product.media.source" :alt="product.name" class="card-img-top"/>
            <h4 class="title text-center card-title display-5">{{product.name}}</h4>
            <p class="description text-center card-text display-5" v-html="product.description"></p>
            <p class="text-center text-muted card-subtitle display-5 price">{{product.price.formatted_with_symbol}}</p>
            <!-- add to cart add to wishlist buttons -->
            <div class="add-btns">
                <button :disabled="isInWishlist" @click="$emit('add-to-wishlist',product)" class="btn btn-info form-control">{{isInWishlist ? 'Added to wishlist': 'Add to Wishlist'}}
                </button>
                <button :disabled="isInCart" @click="$emit('add-to-cart', product)" class="btn btn-info form-control">{{ isInCart ? 'Added to Cart' : 'Add to Cart' }}</button>
            </div><!-- End of Adding btns -->
        </div>
    </div><!-- End of card content -->
</template>

<script>
export default{
    props: ['product','isInCart', 'isInWishlist']
}
</script>

<style>

    .card{
        border: none;
    }

    .card-body img{
        width: 80%;
        display: block;
        margin: 0 auto;
    }

    .card h4{
        padding-top: 20px;
        font-size: 17px;
        font-weight: 700;
        letter-spacing: 2.25px;
        line-height: 32px;
    }


    .add-btns{
        display: flex;
    }

    button.btn{
        background-color: transparent;
        text-decoration: underline;
        border: none;
        color: rgb(60, 60, 60);
        transition: all 0.3s ease-in-out;
    }
    button.btn:hover{
        text-decoration: none;
        background-color: transparent;
        color: #040034;
    }

    button img{
        padding-right: 7px;
    }

    @media only screen and (max-width: 400px){
        .card{
            height: 48rem;
        }

        .add-btns{
            display: block;
        }
    }

</style>