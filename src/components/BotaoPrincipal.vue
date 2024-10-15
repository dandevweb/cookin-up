<script lang="ts">
    export default {
        props: {
            texto: {
                type: String,
                required: true,
            }
        },
    }
</script>

<template>
    <button class="botao-principal paragrafo-lg" @click="$emit('click')">
        {{ texto }}
    </button>
</template>

<style scoped>
.botao-principal {
    background: var(--coral, #F0633C);
    color: var(--creme, #FFFAF3);
    border: none;
    padding: .7rem 2rem;
    border-radius: 1rem;
    font-weight: 700;
    cursor: pointer;
}
</style>
