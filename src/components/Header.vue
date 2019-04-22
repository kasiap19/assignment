<template>
    <div class="container">
        {{products}}
        <div class="header">
            <div class="header__likes">
                <span>{{this.counts}}</span>
            </div>

            <div class="header__list">
                <ul>
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
            likes: [],
            counts: 0
        }
    },

    created() {
        bus.$on('likedProduct', (data) => {
            this.likes = data;
        });

        bus.$on('counter', (data) => {
            this.counts = data
            console.log(this.counts)
        });
    },

    methods: {
        remove(index) {
            this.likes.splice(index, 1);
        }
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
            }

            background: white;
            border: 1px solid $blue;
            height: 30px;
            border-radius: 5px;
            display: flex;
            align-items: center;
            padding: 0 10px;

            span {
                padding: 0 10px;
                text-align: center;
                font-weight: bold;
            }
        }
    }
</style>

