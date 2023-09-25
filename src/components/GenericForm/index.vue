<template>
    <form class="generic-form-wrapper">
        <div class="title-container">
            <h3>Monte aqui o seu cardápio. O que está esperando?</h3>
            <Toggle />
        </div>
        <div class="field-group">
            <input type="text" placeholder="Título do pedido" />
            <input type="text" placeholder="Sabor" />
            <input type="text" placeholder="R$" />
        </div>
        <div class="field-group">
            <textarea placeholder="Descrição"></textarea>
        </div>
        <div class="field-group">
            <label>
                <span class="icon-upload-file"></span>
                <span>Joque aqui o arquivo de imagem do seu pastel ou clique para localizar a pasta.</span>
                <input type="file">
            </label>
        </div>
        <div class="control-container">
            <button class="cancel-button">limpar</button>
            <button type="submit">cadastrar</button>
        </div>
    </form>
</template>
  
<script lang="ts">
export default {
    name: 'GenericForm'
}
</script>
  
<style lang="scss"></style>