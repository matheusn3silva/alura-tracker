<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @ao-tema-alterado="trocarTema" />
    </div>
    
    <div class="column is-three-quarter conteudo">
      <FormularioTracker @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <TarefaTracker v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <BoxContent v-if="listaEstaVazia" >
          Você não está muito produtivo hoje :(
        </BoxContent>
      </div>
      
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import FormularioTracker from './components/Formulario.vue';
import TarefaTracker from './components/Tarefa.vue';
import BoxContent from './components/Box.vue'
import ITarefa from './interfaces/ITarefa';

export default defineComponent({
  name: 'App',
  components: { BarraLateral, FormularioTracker, TarefaTracker, BoxContent },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0
    }
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  }
})
</script>

<style>
.lista {
  padding: 1rem;
}

main {
  --bg-primario: #fff;
  --texto-primario: #000;
}

main.modo-escuro {
  --bg-primario: #2b2b42;
  --texto-primario: #ddd;
}

.conteudo {
  background-color: var(--bg-primario);
}
</style>
