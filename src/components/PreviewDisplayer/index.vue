<template>
    <div class="preview-displayer-wrapper">
        <img class="product-illustration" :src="illustration.src" :alt="illustration.alt">
        <div class="card">
            <div class="title-area">
                <h4>"{{ product.title }}"</h4>
                <div class="price-displayer">R${{ product.price }}</div>
            </div>
            <div class="content">
                <p>
                    <span class="title">Sabor:</span>
                    <span class="value">{{ product.flavor }}</span>
                </p>
                <p v-if="product.description">
                    <span class="title">Descrição:</span>
                    <span class="value">{{ product.description }}</span>
                </p>
            </div>
        </div>
    </div>
</template>
   
<script lang="ts">
import { defineComponent } from 'vue'
import { ProductModel } from '../../model/product.model'
import type { PropType } from 'vue'

export default defineComponent({
    name: 'PreviewDisplayer',
    props:  {
        product: {
            type: Object as PropType<ProductModel>,
            required: true
        }
    },
    computed: {
        illustration() {
            const { imgSrc, type } = this.$props.product
            const defaultSrcBeverage = './suco-img.png'
            const defaultSrcFood = './pastel-img.png'
            return {
                src: imgSrc || (type === 'comida' ? defaultSrcFood : defaultSrcBeverage),
                alt: `ilustracao de ${type}`
            }
        }
    }
})
</script>
   
<style lang="scss" scoped>
    .preview-displayer-wrapper {
        position: relative;
        padding-left: 110px;
        display: flex;
        align-items: center;
        > .card {
            background: white;
            box-shadow: 0px 0px 30px #740B0B45;
            border-radius: 20px;
            flex-grow: 1;
            > * {
                padding-right: 32px;
                padding-left: 110px;
            }
        }
    }
    .title-area {
        background: #E43636;
        border-radius: 20px 20px 0px 0px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-weight: bold;
        font-style: italic;
        min-height: 80px;
        h4 {
            color: #FFCA00;
            font-size: 30px;
            line-height: 37px;
            margin: 0;
        }
        .price-displayer {
            font-size: 26px;
            line-height: 32px;
            color: #FFFFFF;
        }
    }
    .content {
        padding: 30px 0 16px;
        color: #A03400;
        min-height: 140px;
        p {
            margin: 0 0 14px 0;
        }
        .title {
            font-size: 24px;
            font-style: italic;
        }
        .value {
            font-size: 24px;
            margin-left: 0.5em;
        }
    }
    .product-illustration {
        object-fit: none;
        width: 180px;
        height: 180px;
        position: absolute;
        left: 0;
        border-radius: 10px;
        overflow: hidden;
    }
</style>