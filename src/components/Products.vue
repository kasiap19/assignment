<template>
    <div class="products-component">
        <div class="container products">
            <div class="products__title">
                <h1>results</h1>
            </div>
            <div class="products__content">
                <div class="product" v-for="product in products" :key="product.id">
                    <div class="product__img" :style="{ backgroundImage: 'url(' + product.img + ')' }"></div>
                    <div class="product__likes">
                        <button @click="like(product.title)"></button>
                    </div>
                    <div class="product__desc desc"> 
                        <div class="desc__title">
                            <h3>{{product.title}}</h3>
                            <span>{{product.brand}}</span>
                        </div>
                        <div class="desc__sum">
                            <span>size: {{product.size}}</span>
                            <span class="desc__sum--price">{{product.price}} £</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Products',
    props: ['products'],
    data() {
        return {
            liked: []
        }
    },
    methods: {
        like(a) {
            event.target.parentNode.parentNode.classList.add('is-active')
            this.liked.push(a)

            console.log(this.liked)
        }
    }
}
</script>

<style lang="scss">
@import '../assets/_settings.scss';

.products-component {
    background: #f1f2f6;
    padding: 50px 0;
}

.products {

    &__title {
        h1 {
            text-transform: uppercase;
            font-weight: 900;
            font-size: 26px; 
        }
    }
    
    &__content {
        display: grid;
        grid-row-gap: 16px;

        @include md {
            grid-template-columns: repeat(2, 1fr);
            grid-gap: 16px;
        }

        @include lg {
            grid-template-columns: repeat(4, 1fr);
            grid-gap: 32px;
        }
    }
}

.product {
    position: relative;
    background: white;

    &.is-active {
        button {
            &:before {
                color: white;
            }
            
            background: darkred;
            border: 1px solid darkred;
        }
    }

    &__img {
        height: 150px;
        background-size: cover;
        background-position: center;
        border-radius: 5px 5px 0 0;
    }

    &__desc {
        padding: 20px;
    }

    &__likes {
        position: absolute;
        top: 10px;
        right: 10px;

        button {
            &:before {
                content: '\f164';
                font-family: "Font Awesome 5 Free";
                font-size: 15px;
                color: $blue;
                font-weight: bold;
                transition: 0;
            }

            &:focus {
                outline: 0;
            }

            border-radius: 5px;
            padding: 7px;
            background: white;

            &:hover {
                background: darkred;
                border: 1px solid darkred;
                transition: .3s;
                cursor: pointer;

                &:before {
                    color: white;
                }
            }
        }
    }
}

.desc {
    &__title {
        height: 50px;
        display: flex;
        justify-content: space-between;
        align-items: center;

        h3 {
            font-size: 16px;
        }

        span {
            font-size: 13px;
            font-weight: 400;
            font-style: italic;
        }
    }

    &__sum {
        display: flex;
        justify-content: space-between;
        align-items: center;

        &--price {
            font-size: 24px;
            font-weight: 600;
        }
    }
}

</style>
