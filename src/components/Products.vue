<template>
    <div class="products-component">
        <div class="container products">
            <div class="products__title">
                <h1>results</h1>
                <button @click="hideItems" v-if="hideSold">hide sold items</button>
                <button @click="all" v-if="showAll">show all</button>
            </div>
            <div class="products__content">
                <div v-for="product in products" :key="product.id" :class="{'sold': product.sold}">
                    <div class="product" >
                        <div class="sold__content" v-if="product.sold === true">
                            <h4>sold</h4>
                        </div>
                        <div class="product__img" :style="{ backgroundImage: 'url(' + product.img + ')' }"></div>

                        <!-- likes -->
                        <div class="product__likes">
                            <div v-for="i in liked" :class="{'colored': product.title === i}"></div>
                            <div class="button" @click="like(product.title)" ></div>
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
    </div>
</template>

<script>
import { bus } from '../main';

export default { 
    name: 'Products',
    props: {
        products: {
            type: Array
        },
    },

    data() {
        return {
            liked: [],
            counter: 1,
            hideSold: true,
            showAll: false
        }
    },
    mounted() {
        bus.$on('removed', (data) => {
            this.liked = data;
            console.log(this.liked)    
        });
    },

    methods: {
        like(a) {
            // event.target.parentNode.parentNode.classList.add('is-active')
            this.liked.push(a)

            bus.$emit('likedProduct', this.liked);
            bus.$emit('counter', this.counter)

            this.counter +=1

            // console.log(this.liked)

        },

        hideItems() {
            const items = document.getElementsByClassName('sold');

            for(this.item of items){
                this.item.classList.add('fade');
            }

            this.hideSold = false;
            this.showAll = true;
        },

        all() {
            const items = document.getElementsByClassName('sold');

            for(this.item of items){
                this.item.classList.remove('fade');
            }

            this.hideSold = true;
            this.showAll = false;
        }
    }
}
</script>

<style lang="scss">
@import '../assets/_settings.scss';

button {
    &:focus {
        outline: 0;
    }
}

.products-component {
    background: #f1f2f6;
    padding: 50px 0;
}

.products {

    &.closeBtn {
        .products__title {
            button {
                display: none;
            }
        }
    }

    &__title {
        display: flex;
        justify-content: space-between;
        align-items: center;

        h1 {
            text-transform: uppercase;
            font-weight: 900;
            font-size: 26px; 
        }

        button {
            background: transparent;
            height: 40px;
            color: $blue;
            border: 1px solid $blue;
            text-transform: uppercase;
            font-weight: bold;
            border-radius: 5px;
            color: $blue;
            padding: 0 15px;
            transition: .3s;

            &:hover {
                background: $blue;
                color: white;
                cursor: pointer;
            }
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

        .button {
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

.sold {

    &.fade {
        display: none;
    }

    &__content {
        &:after {
            content: '';
            background: rgba(1,1,1, .5);
            position: absolute;
            width: 100%;
            height: 100%;
            border-top-left-radius: 5px;
            border-top-right-radius: 5px;
            z-index: 0;
            top: 0;
        }

        position: absolute;
        width: 100%;
        height: 150px;
        display: flex;
        justify-content: center;
        align-items: center;

        h4 {
            color: white;
            z-index: 111;
            text-transform: uppercase;
            border: 1px solid #ddd;
            padding: 10px;
        }
    }
}

.colored {
     &:before {
        content: '\f164';
        font-family: "Font Awesome 5 Free";
        font-size: 15px;
        color: white;
        font-weight: bold;
        transition: 0;
    }

    background: darkred;
    border-radius: 5px;
    position: absolute;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
}

</style>
