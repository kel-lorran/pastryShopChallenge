<template>
    <form class="generic-form-wrapper" @submit.prevent="saveProduct" ref="productForm">
        <div class="title-container">
            <h3>Monte aqui o seu cardápio. O que está esperando?</h3>
            <div class="toggle-container">
                <span>Comida</span>
                <switches :value="toggle" v-on:change="changeType"></switches>
                <span>Bebida</span>
            </div>
        </div>
        <div class="field-group first">
            <input type="text" v-model="title" placeholder="Título do pedido" required />
            <input type="text" v-model="flavor" placeholder="Sabor" required />
            <input type="text" @input="sanitizePrice" placeholder="R$" required />
        </div>
        <div class="field-group">
            <textarea v-model="description" placeholder="Descrição"></textarea>
        </div>
        <div class="field-group file">
            <label>
                <span class="icon-upload-file"></span>
                <span v-if="!imgSrc">Joque aqui o arquivo de imagem do seu pastel ou clique para localizar a pasta.</span>
                <span v-else>Um arquivo selecionado!.</span>
                <input @change="uploadImage" type="file">
            </label>
        </div>
        <div class="control-container">

            <button class="cancel-button" @click.prevent="clearForm">limpar</button>
            <button class="submit-button" :disabled="desableSubmit" type="submit">cadastrar</button>
        </div>
    </form>
</template>
  
<script lang="ts">
import Switches from 'vue-switches';
const initialParcialData = {
    title: '',
    flavor: '',
    price: '',
    description: '',
    imgSrc: '',
    toggle: false,
}
export default {
    name: 'GenericForm',
    data () {
        return {
            ...initialParcialData,
            type: 'comida',
        }
    },
    components: {
        Switches
    },
    computed: {
        desableSubmit() {
            const { title, flavor, price } = this.$data
            return !(title && flavor && price)
        }
    },
    methods: {
        changeType() {
            this.$data.toggle = !this.$data.toggle
            const currentType = this.$data.type
            this.$data.type = currentType === 'comida' ? 'bebida' : 'comida'
        },
        uploadImage(event: Event) {
            const files = (event.target as HTMLInputElement).files;
            const fr = new FileReader();
            if(files) {
                fr.onload = () => {
                    this.$data.imgSrc = fr.result?.toString() || ''
                }
                fr.readAsDataURL(files[0]);
            }
        },
        saveProduct() {
            this.$emit("saveProduct", {
                title: this.$data.title,
                flavor: this.$data.flavor,
                price: this.$data.price,
                description: this.$data.description,
                imgSrc: this.$data.imgSrc,
                type: this.$data.type,
            })
            this.clearForm()
        },
        clearForm() {
            Object.assign(this.$data, initialParcialData);
            (this.$refs.productForm as HTMLFormElement).reset()
        },
        sanitizePrice(event: Event) {
            const value = (event.target as HTMLInputElement).value;
            const newValue = value.replace(/[^0-9]/g, '');
            (event.target as HTMLInputElement).value = `R$${newValue}`
            this.$data.price = newValue
        }
    }
}
</script>
  
<style lang="scss" scoped>
    .generic-form-wrapper {
        background: white;
        box-shadow: 0px 0px 30px #740B0B45;
        border-radius: 20px;
        margin-bottom: 100px;
        > * {
            padding: 0 20px;
        }
    }
    .title-container {
        min-height: 93px;
        background: #FFCA00 0% 0% no-repeat padding-box;
        border-radius: 20px 20px 0px 0px;
        display: flex;
        align-items: center;
        color: #A03400;
        font-style: italic;
        padding-left: 60px;
        display: flex;
        justify-content: space-between;
    }
    $inputHeight: 40px;
    @mixin inputStyle {
        border: 1px solid #E43636;
        border-radius: 10px;
        font-size: 16px;
        line-height: 21px;
        color: #A03400;
        padding: 10px 20px;
        width: 100%;
    }
    input, textarea {
        @include inputStyle;
        &::placeholder {
            color: #A03400;
        }
    }
    .field-group {
        margin-bottom: 20px;
        display: flex;
        justify-content: space-between;
        gap: 20px;
        &.first {
            margin-top: calc(#{$inputHeight} / -2);
            input:nth-of-type(1) {
                width: 42%;
            }
            input:nth-of-type(2) {
                width: 43%;
            }
            input:nth-of-type(3) {
                width: 18%;
            }
            input {
                padding: 0 20px;
                height: $inputHeight;
            }
        }
        &.file {
            input {
                display: none;
            }
            label {
                @include inputStyle;
                display: flex;
                flex-direction: column;
                align-items: center;
                justify-content: center;
                padding: 20px;
                min-height: 110px;
            }
        }
    }
    textarea {
        min-height: 80px;
    }
    .icon-upload-file {
        display: block;
        width: 48px;
        height: 44px;
        background: url(../../assets/upload.png) no-repeat center;
        background-size: contain;
    }
    $buttonHeight: 60px;
    button {
        border: none;
        font-size: 20px;
        text-transform: uppercase;
        height: $buttonHeight;
        width: 200px;
        border-radius: calc(#{$buttonHeight} / 2);
        font-weight: bold;
        & + button {
            margin-left: 34px;
        }
        &[disabled] {
            filter: grayscale(0.8);
            cursor: no-drop;
        }
        &:hover {
            opacity: 0.95;
        }
        &:active {
            opacity: 0.7;
        }
    }
    .control-container {
        display: flex;
        justify-content: center;
        position: relative;
        bottom: calc(60px / -2);
        margin-top: calc(60px / -2);
    }
    .cancel-button {
        background: #E43636;
        color: white;
    }
    .submit-button {
        background: #FFCA00;
        color: #A03400;
    }
    .toggle-container{
        display: flex;
        align-items: center;
        > span {
            font-size: 16px;
            margin: 0 0.8em;
        }
    }
</style>
<style lang="scss">
    .vue-switcher {
        > div {
            background-color: white !important;
            &::after {
                background-color: #E33535 !important;
            }
        }
    }
</style>