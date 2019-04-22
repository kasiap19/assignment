<template>
    <div class="container">
        <div class="header">
            <button>
                <span>xx</span>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Header'
}
</script>

<style lang="scss" scoped>
@import '../assets/_settings.scss';

    .header {
        display: flex;
        height: 50px;
        justify-content: flex-end;
        align-items: center;

        button {
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

            span {
                padding: 0 10px;
                text-align: center;
            }
        }
    }
</style>

