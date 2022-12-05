<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro' : modoEscuro}">
    <div class="column is-one-quarter">
      <BarraLateral @aoAlterarModo="alterarModo"/>
    </div>

    <div class="column is-three-quarters conteudo">
      <FormularioTarefa @aoSalvarTarefa="salvarTarefa" />
      <div class="listaTarefa">
        <ListaTarefa v-for="(listaTarefa, index) in listaTarefas" :listaTarefa="listaTarefa" :key="index"/>
        <TemplateBox v-if="semTarefas">
          <strong>
            Você não está muito produtivo hoje :(
          </strong>
        </TemplateBox>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue'
import FormularioTarefa from './components/FormularioTarefa.vue'
import ListaTarefa from './components/ListaTarefa.vue'
import IListaTarefa from  './interfaces/IListaTarefa'
import TemplateBox from  './components/TemplateBox.vue'

export default defineComponent({
  name: 'App',
  components: {
    BarraLateral,
    FormularioTarefa,
    ListaTarefa,
    TemplateBox
  },
  data () {
    return {
      listaTarefas: [] as IListaTarefa[],
      modoEscuro: false
    }
  },
  computed: {
    semTarefas () :boolean {
      return this.listaTarefas.length == 0
    }
  },
  methods: {
    salvarTarefa (listaTarefa: IListaTarefa) {
      this.listaTarefas.push(listaTarefa)
    },
    alterarModo (modoEscuro: boolean) : void {
      this.modoEscuro = modoEscuro
    }
  },
});
</script>

<style>
  main {
    --bg-primario: #fff;
    --texto-primario: #2b2d42;
  }
  main.modo-escuro {
    --bg-primario: #2b2d42;
    --texto-primario: #ddd;
  }
  strong {
    color: #2b2d42;
  }
  .conteudo {
    background-color: var(--bg-primario);
  }
  .listaTarefa {
        padding: 1.25rem;
    }
</style>
