<script lang="ts">
import { defineComponent } from 'vue';
import Formulario from '../components/Formulario.vue';
import Tarefa from '../components/Tarefa.vue';
import Box from '../components/Box.vue';
import ITarefa from '@/interfaces/ITarefa';



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
    }   

  },

  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0
    }
  },
  components: {  Formulario, Tarefa, Box }

});
</script>



<template>
      <Formulario @aoSalvarTarefa="salvarTarefa" />
     
      <div class="lista">
        <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <Box v-if="listaEstaVazia">
          Você não está muito produtivo hoje :(
        </Box>
      </div>
</template>




