<script lang="ts">
import { defineComponent } from "vue";
import Cronometro from "./Cronometro.vue";

export default defineComponent({
    name: 'Temporizador',
    emits: ['aoTemporizadorFinalizado'],
   
    
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        }
    },

    methods: {
        iniciar() {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1
            }, 1000)

        },
        finalizar() {
            this.cronometroRodando = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0

        }
    },
             components: { Cronometro }
})
</script>

<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        
        <Cronometro :tempoEmSegundos="tempoEmSegundos" />
        
        <button class="button" @click="iniciar" texto="play" 
        :disabled="cronometroRodando">
         <span class="icon">
         <i class="fas fa-play"></i>
        </span>
         <span>Play</span>
        </button>

        
        <button class="button" @click="finalizar" texto="stop" 
        :disabled="!cronometroRodando">
         <span class="icon">
         <i class="fas fa-stop"></i>
         </span>
         <span>Stop</span>
        </button>
    </div>
</template>