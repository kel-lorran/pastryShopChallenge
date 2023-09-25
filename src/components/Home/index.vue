<template>
    <main class="home-page">
        <div class="container">
            <GenericForm />
        </div>
        <h3>Veja como será apresentado ao cliente</h3>
        <PreviewDisplayer></PreviewDisplayer>
    </main>
</template>
  
<script lang="ts">
import GenericForm from '../GenericForm/index.vue'
import PreviewDisplayer from '../PreviewDisplayer/index.vue'

export default {
    name: 'Home',
    // props: {
    //     //   isRegisterMoment:{
    //     //     Type: Boolean,
    //     //     default: false
    //     //   }
    // },
    data() {
        return {
        }
    },
    mounted() {},
    computed: {},
    methods: {
    },
    components: {
        GenericForm,
        PreviewDisplayer
    }
}
</script>
  
<style lang="scss"></style>