<script>
export default {
  props: {
    tarefas: Array,
  },
  emits: ["alterouStatus", "removeuElemento"],
  methods: {
    alteraStatus(e) {
      let tarefaEncontrada = this.tarefas.find((tarefa) => {
        return tarefa.id === parseInt(e.target.id);
      });
      tarefaEncontrada.concluida = e.target.checked;
      this.$emit("alterouStatus");
    },
    remover(id) {
      const arrayFiltrado = this.tarefas.filter((e) => e.id !== id);
      this.$emit("removeuElemento", arrayFiltrado);
    },
  },
};
</script>

<template>
  <p class="titulo">Lista de tarefas:</p>
  <ul v-if="tarefas.length > 0">
    <li v-for="tarefa in tarefas" :key="tarefa.id">
      <input
        type="checkbox"
        :name="tarefa.id"
        :id="tarefa.id"
        :checked="tarefa.concluida"
        @change="alteraStatus($event)"
      />
      <label :for="tarefa.id">{{ tarefa.nome }}</label>
      <button class="btn-remover" title="Remover" @click="remover(tarefa.id)">
        X
      </button>
    </li>
  </ul>
  <p v-else><strong>Nenhuma tarefa adicionada!</strong></p>
</template>

<style scoped>
.titulo {
  margin: 40px 0 0 0;
}
ul {
  width: 400px;
  padding: 0;
  list-style: none;
  margin: 0 10px;
}
li {
  padding: 5px;
}

label {
  cursor: pointer;
}
.btn-remover {
  width: 27px;
  height: 24px;
  border-radius: 5px;
  margin: 0px 5px;
  background: #b82727;
  color: #fff;
  border: nonte;
  border: none;
  cursor: pointer;
}

.btn-remover:hover {
  background: #cf4c4c;
}
</style>
