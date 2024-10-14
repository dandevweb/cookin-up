<script lang="ts">
    export default {
        props: {
            texto: {
                type: String,
                required: true,
            },
            ativo: Boolean
        },
    }
</script>

<template>
    <span class="tag" :class="{ ativo }">
        {{ texto }}
    </span>
</template>

<style scoped>
.tag {
  display: inline-block;
  border-radius: 0.5rem;
  min-width: 4.25rem;
  padding: 0.5rem;
  text-align: center;
    transition: 0.2s;
    background: var(--cinza-claro, #EFEFEF);
    color: var(--cinza, #444);
    font-weight: 400;
}

.ativo {
    background: var(--coral, #F0633C);
    color: var(--creme, #FFFAF3);
    font-weight: 700;
}
</style>
