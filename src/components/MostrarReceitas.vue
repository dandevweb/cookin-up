<script lang="ts">
import { obterReceitas } from '@/http/index';
import type IReceita from '@/interfaces/IReceita';
import CardReceita from './CardReceita.vue';
import BotaoPrincipal from './BotaoPrincipal.vue';
import type { PropType } from 'vue';
import { itensDeLista1EstaoEmLista2 } from '@/operacoes/listas';

    export default {
        props: {
            ingredientes: {
                type: Array as PropType<string[]>,
                required: true,
            }
        },
        data() {
            return {
                receitas: [] as IReceita[],
            }
        },
        async created() {
           const receitas = await obterReceitas();

           this.receitas = receitas.filter((receita) => {
            const possoFazerReceita = itensDeLista1EstaoEmLista2(receita.ingredientes, this.ingredientes);

            return possoFazerReceita;
           })
        },
        components: {
            CardReceita,
            BotaoPrincipal,
        },
        emits: ['SelecionarIngredientes'],
    }
</script>

<template>
   <section class="selecionar-ingredientes">
        <h1 class="cabecalho titulo-ingredientes">
            Receitas
        </h1>
        <p>Resultados encontrados: {{ receitas.length }}</p>

       <div v-if="receitas.length">
            <p class="paragrafo-lg instrucoes">Veja as opções de receitas que encontramos com os ingredientes que você tem por aí.</p>

            <ul class="receitas">
                <li v-for="receita in receitas" :key="receita.nome">
                    <CardReceita
                    :receita="receita"
                    />
                </li>
            </ul>
       </div>

        <div v-else class="paragrafo dica">
            <p>Ops, não encontramos resultados para sua combinação. Vamos tentar de novo?</p>
            <img src="../assets/imagens/sem-receitas.png" alt="Lista vazia">
        </div>

        <BotaoPrincipal texto="Editar Lista" @click="$emit('SelecionarIngredientes')"/>
    </section>
</template>

<style scoped>
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  color: var(--verde-medio, #3D6D4A);
  display: block;
  margin-bottom: 1.5rem;
}

.receitas {
    margin-top: 1rem;
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}
</style>
