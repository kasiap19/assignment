<template>
    <div class="container">
        {{products}}
        <div class="header">
            <div class="header__likes" @click="showLiked">
                <span>{{this.counts}}</span>
            </div>

            <div class="header__list" >
                <ul v-if="active">
                    <li v-for="(like, index) in likes">
                        <span> {{like}}</span>
                        <button @click="remove(index)">X</button>

                    </li>
                </ul>
            </div>
            
        </div>
    </div>
</template>

<script>
import { bus } from '../main';

export default {
    name: 'Header',
    props: ['products'],

    data() {
        return {
            active: false,
            likes: [],
            counts: 0
        }
    },

    created() {
        bus.$on('likedProduct', (data) => {
            this.likes = data;

            console.log(this.likes.length)
        });

        bus.$on('counter', (data) => {
            this.counts = data 
            // console.log(this.counts)
        });
    },

    methods: {
        remove(index) {
            this.likes.splice(index, 1);
            this.counts = this.likes.length

            bus.$emit('removed', this.likes); 
        },
        showLiked() {
            this.active = !this.active; 
        },
    }
}
</script>

<style lang="scss" scoped>
@import '../assets/_settings.scss';

    .header {
        display: flex;
        flex-direction: column;
        height: 50px;
        justify-content: center;
        align-items: flex-end;

        &__list {
            z-index: 1;
            position: absolute;
            top: 30px;
            right: 90px;

            ul {
                list-style: none;
                background: white;
                // border: 1px solid $blue;
                border-radius: 5px;
                padding: 10px 0;

                li {
                    padding: 0 5px 0 20px;
                    font-size: 12px;
                    min-height: 30px;
                    display: flex;
                    justify-content: space-between;
                    align-items: center;
                    font-weight: bold;

                    &:hover {
                        button {
                            opacity: 1;
                        }
                    }
                }

                button {
                    background: transparent;
                    border: none;
                    font-weight: bold;
                    color: darkred;
                    padding: 0 10px;
                    transition: .3s;

                    @include lg {
                        opacity: 0;
                    }

                    &:hover {
                        cursor: pointer;
                    }
                }
            }
        }

        &__likes {
            &:before {
                content: '\f164';
                font-family: "Font Awesome 5 Free";
                font-size: 15px;
                color: $blue;
                font-weight: bold;
                transition: 0;
                pointer-events: none;
            }

            background: white;
            border: 1px solid $blue;
            height: 30px;
            border-radius: 5px;
            display: flex;
            align-items: center;
            padding: 0 10px;
            pointer-events: visible;
            transition: .3s;

            &:hover {
                &:before {
                    color: white;
                }

                background: $blue;
                color: white;
                cursor: pointer;
            }

            span {
                padding: 0 10px;
                text-align: center;
                font-weight: bold;
                pointer-events: none;
            }

        }
    }
</style>

