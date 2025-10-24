<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import Notificacoes from './components/Notificacoes.vue';

export default defineComponent({
  name: 'App',

  data() {
    return {
    
      modoEscutoAtivo: false
    }

  },
  methods: {
    
    trocarTema(modoEscuroAtivo: boolean) {
     this.modoEscutoAtivo = modoEscuroAtivo
    }

  },

  
  components: { BarraLateral, Notificacoes }

});
</script>



<template>
  <main class="columns is-gapless is-multiline " :class="{'modo-escuro': modoEscutoAtivo}">

    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
      <div class="lista"></div>

    </div>

    <div class="column is-three-quarters conteudo">
      <Notificacoes/>
      <RouterView/>
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


