<template>
    <main class="home-page">
        <img class="logo-img" src="../../assets/logo.png" alt="logo" />
        <div class="container form-container">
            <GenericForm @saveProduct="addProduct" />
        </div>
        <h3><span>Veja como será apresentado ao cliente</span></h3>

        <div class="container preview-container">
            <div class="displayer-slot" v-for="(item, index) in productList">
                <PreviewDisplayer :product="item"></PreviewDisplayer>
                <svg xmlns="http://www.w3.org/2000/svg" @click="() => removeProduct(index)" height="1em"
                    viewBox="0 0 448 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
                    <path
                        d="M170.5 51.6L151.5 80h145l-19-28.4c-1.5-2.2-4-3.6-6.7-3.6H177.1c-2.7 0-5.2 1.3-6.7 3.6zm147-26.6L354.2 80H368h48 8c13.3 0 24 10.7 24 24s-10.7 24-24 24h-8V432c0 44.2-35.8 80-80 80H112c-44.2 0-80-35.8-80-80V128H24c-13.3 0-24-10.7-24-24S10.7 80 24 80h8H80 93.8l36.7-55.1C140.9 9.4 158.4 0 177.1 0h93.7c18.7 0 36.2 9.4 46.6 24.9zM80 128V432c0 17.7 14.3 32 32 32H336c17.7 0 32-14.3 32-32V128H80zm80 64V400c0 8.8-7.2 16-16 16s-16-7.2-16-16V192c0-8.8 7.2-16 16-16s16 7.2 16 16zm80 0V400c0 8.8-7.2 16-16 16s-16-7.2-16-16V192c0-8.8 7.2-16 16-16s16 7.2 16 16zm80 0V400c0 8.8-7.2 16-16 16s-16-7.2-16-16V192c0-8.8 7.2-16 16-16s16 7.2 16 16z" />
                </svg>
            </div>
        </div>
    </main>
</template>

<script lang="ts">
import GenericForm from "../GenericForm/index.vue";
import PreviewDisplayer from "../PreviewDisplayer/index.vue";
import { ProductModel } from "../../model/product.model";

export default {
    name: "Home",
    data(): {
        productList: ProductModel[];
    } {
        return {
            productList: [],
        };
    },
    methods: {
        addProduct(event: ProductModel) {
            this.$data.productList = [...this.$data.productList, event];
        },
        removeProduct(index: number) {
            const tempProductList = [...this.$data.productList]
            tempProductList.splice(index, 1)
            this.$data.productList = tempProductList;
        }
    },
    components: {
        GenericForm,
        PreviewDisplayer,
    },
};
</script>

<style lang="scss" scoped>
$marginContainer: 16px;
$widthContainer: 1180px;

.container {
    margin: $marginContainer auto;
    max-width: $widthContainer;
    width: 100%;
}

.preview-container {
    >*+* {
        margin-top: 30px;
    }
}

.home-page {
    display: flex;
    flex-direction: column;
    align-items: center;
    background: url(../../assets/pattern.png) repeat center;
    position: relative;
    padding-bottom: 74px;

    &::before {
        content: "";
        background: url(../../assets/wave.png) no-repeat center bottom;
        position: absolute;
        top: 0;
        height: 546px;
        left: 0;
        right: 0;
        background-size: cover;
        z-index: 2;
    }

    &::after {
        content: "";
        position: absolute;
        top: 0;
        width: $widthContainer;
        bottom: 0;
        background: white;
        z-index: -2;
        box-shadow: 0px 0px 79px 125px rgba(255, 255, 255, 1);
        z-index: 1;
    }

    >* {
        z-index: 5;
    }
}

.logo-img {
    margin: 60px 0 24px;
}

$colorPreviweTitle: #a03400;

h3 {
    text-align: center;
    font-size: 24px;
    font-style: italic;
    letter-spacing: 0px;
    color: $colorPreviweTitle;
    display: flex;
    align-items: center;

    &::before {
        content: "";
        position: absolute;
        height: 1px;
        background: $colorPreviweTitle;
        left: 0;
        right: 0;
    }

    span {
        background: white;
        z-index: 5;
        padding: 0 2em;
    }
}

.displayer-slot {
    position: relative;

    svg {
        position: absolute;
        right: -1.5em;
        top: 0.5em;
        font-size: 24px;
        fill: $colorPreviweTitle;
        cursor: pointer;
    }
}
</style>
