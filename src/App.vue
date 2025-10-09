<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import MeuFormulario from './components/MeuFormulario.vue';
import Tarefa from './components/Tarefa.vue';
import ITarefa from './interfaces/ITarefa';
import Box from './components/Box.vue';



export default defineComponent({
  name: 'App',

  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscutoAtivo: false
    }

  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocarTema(modoEscuroAtivo: boolean) {
     this.modoEscutoAtivo = modoEscuroAtivo
    }

  },

  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0
    }
  },
  components: { BarraLateral, MeuFormulario, Tarefa, Box }

});
</script>



<template>
  <main class="columns is-gapless is-multiline " :class="{'modo-escuro': modoEscutoAtivo}">

    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
      <div class="lista"></div>

    </div>

    <div class="column is-three-quarter conteudo">
      <MeuFormulario @aoSalvarTarefa="salvarTarefa" />

      <div class="lista">

        <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <Box v-if="listaEstaVazia">
          Você não está muito produtivo hoje :(
        </Box>
      </div>
    </div>
  </main>
</template>

<style>
.lista{
  padding: 1.25rem;
}

main{
  --bg-primario: #ffff;
  --texto-primario: #0000;
}

main.modo-escuro{
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}
.conteudo{
  background-color: var(--bg-primario);
}

</style>


