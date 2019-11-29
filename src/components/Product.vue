<!-- Products -->
<template>
    <div class="card my-5 border-0" style="height:41rem;">
        <div class="card-body">
            <img :src="product.media.source" :alt="product.name" class="card-img-top"/>
            <h4 class="title text-center card-title display-5 pt-4">{{product.name}}</h4>
            <p class="description text-center card-text display-5" v-html="product.description"></p>
            <p class="text-center text-muted card-subtitle display-5 price">{{product.price.formatted_with_symbol}}</p>
            <!-- add to cart button -->
            <div class="add-btns d-flex">
                <button :disabled="isInCart" 
                        @click="$emit('add-to-cart', product)"
                        class="btn btn-info form-control">
                        {{ isInCart ? 'Added to Cart' : 'Add to Cart' }}
                </button>
            </div><!-- End of Adding btn -->
        </div>
    </div><!-- End of card content -->
</template>

<script>
export default{
    name: 'product',
    props: ['product','isInCart']
}
</script>

<style>

    .card-body img{
        width: 80%;
        display: block;
        margin: 0 auto;
    }

    .card h4{
        font-size: 17px;
        font-weight: 700;
        letter-spacing: 2.25px;
        line-height: 32px;
    }

    button.btn{
        background-color: transparent;
        text-decoration: underline;
        border: none;
        color: rgb(60, 60, 60);
    }
    button.btn:hover{
        text-decoration: none;
        background-color: transparent;
        color: #040034;
    }

</style>