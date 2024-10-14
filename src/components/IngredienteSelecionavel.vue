<script lang="ts">
import Tag from './Tag.vue';

    export default {
        props: {
            ingrediente: {
                type: String,
                required: true,
            },
        },
        components: {
            Tag,
        },
        data() {
            return {
                selecionado: false,
            }
        },
        methods: {
            aoClicar() {
                this.selecionado = !this.selecionado

                if (this.selecionado) {
                    this.$emit('adicionarIngrediente', this.ingrediente)
                } else {
                    this.$emit('removerIngrediente', this.ingrediente)
                }
            }
        },
        emits: ['adicionarIngrediente', 'removerIngrediente'],
    }
</script>

<template>
    <button
        v-on:click="aoClicar"
        :aria-pressed="selecionado"
        class="ingredient">
        <Tag :texto="ingrediente" :ativo="selecionado" />
    </button>
</template>

<style scoped>
.ingredient {
    cursor: pointer;
}
</style>
