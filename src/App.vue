<script setup>
import NovaTarefa from "./components/NovaTarefa.vue";
import ListaTarefas from "./components/ListaTarefas.vue";
import BarraProgresso from "./components/BarraProgresso.vue";
</script>

<script>
export default {
  components: {
    NovaTarefa,
    ListaTarefas,
    BarraProgresso,
  },
  data() {
    return {
      tarefas: [],
    };
  },
  methods: {
    removerElemento(tarefas) {
      this.tarefas = tarefas;
      this.atualizaLocalStorage();
    },
    atualizaLocalStorage() {
      localStorage.setItem("tarefas", JSON.stringify(this.tarefas));
    },
  },
  mounted() {
    this.tarefas = JSON.parse(localStorage.getItem("tarefas")) || [];
  },
};
</script>

<template>
  <div class="container">
    <BarraProgresso :tarefas="tarefas" />
    <NovaTarefa :tarefas="tarefas" @tarefaAdicionada="atualizaLocalStorage" />
    <ListaTarefas
      :tarefas="tarefas"
      @alterouStatus="atualizaLocalStorage"
      @removeuElemento="removerElemento($event)"
    />
  </div>
</template>

<style scoped>
.container {
  width: 100vw;
  height: auto;
  margin: 4% auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
