<script lang="ts">
import { defineComponent } from 'vue';
import Temporizador from './Temporizador.vue';

export default defineComponent({
    name: 'MeuFormulario',
    emits: ['aoSalvarTarefa'],
    data() {
        return {
            descricao: ''
        }
    },

    methods: {
        finalizarTarefa(tempoDeCorrido: number): void {
            this.$emit('aoSalvarTarefa',
                {
                    duracaoEmSegundos: tempoDeCorrido,
                    descricao: this.descricao
                })
            this.descricao = ''
        }
    },

    components: { Temporizador }

})
</script>


<template>
    <div class="box formulario">
       
        <div class="columns">
            
            <div class="column is-8" role="form" 
            aria-label="Formulário para criação de uma nova tarefa">
            
            <input type="text" class="input" 
            placeholder="Qual tarefa você deseja iniciar?" 
            v-model="descricao" />
            </div>
            
            <div class="column">
                <Temporizador
                 @ao-temporizador-finalizado="finalizarTarefa" />
            </div>
            </div>
            </div>
</template>

<style>
.formulario{
   color: var(--texto-primario); 
   background-color: var(--bg-primario);
}
</style>



