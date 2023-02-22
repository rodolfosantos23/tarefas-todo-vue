<script setup>
import NovaTarefa from "./components/NovaTarefa.vue";
import ListaTarefas from "./components/ListaTarefas.vue";
import BarraTarefasConcluidas from "./components/BarraTarefasConcluidas.vue";
</script>

<script>
export default {
  components: {
    NovaTarefa,
    ListaTarefas,
    BarraTarefasConcluidas,
  },
  data() {
    return {
      tarefas: [],
      porcentagem: 0,
      tarefasConcluidas: 0,
      totalTarefas: 0,
    };
  },
  methods: {
    adicionarTarefa(tarefa) {
      this.tarefas.push(tarefa);
      this.calculaPorcentagem();
    },
    calculaPorcentagem() {
      this.totalTarefas = this.tarefas.length;
      this.tarefasConcluidas = 0;
      this.tarefas.forEach((t) => {
        if (t.concluida) {
          this.tarefasConcluidas++;
        }
      });

      if (this.tarefasConcluidas == 0) {
        this.porcentagem = 0;
      } else {
        this.porcentagem = (this.tarefasConcluidas / this.totalTarefas) * 100;
      }
      this.atualizaLocalStorage();
    },
    removerElemento(tarefas) {
      this.tarefas = tarefas;
      this.calculaPorcentagem();
    },
    atualizaLocalStorage() {
      localStorage.setItem("tarefas", JSON.stringify(this.tarefas));
    },
  },
  mounted() {
    const tarefasLocal = JSON.parse(localStorage.getItem("tarefas"));
    if (tarefasLocal.length > 0) {
      this.tarefas = tarefasLocal;
      this.calculaPorcentagem();
    } else {
      this.tarefas = [];
    }
  },
};
</script>

<template>
  <div class="container">
    <h3>Tarefas:</h3>
    <BarraTarefasConcluidas :porcentagem="porcentagem" />
    <NovaTarefa @tarefaAdicionada="adicionarTarefa($event)" />
    <ListaTarefas
      :tarefas="tarefas"
      @alterouStatus="calculaPorcentagem"
      @removeuElemento="removerElemento($event)"
    />
  </div>
</template>

<style scoped>
.container {
  width: 100vw;
  height: auto;
  margin: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
