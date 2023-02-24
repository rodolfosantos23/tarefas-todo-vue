<script>
export default {
  props: {
    tarefas: {
      type: Array,
      required: true,
    },
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
  <div v-if="tarefas.length > 0">
    <table border="1">
      <tr v-for="(tarefa, index) in tarefas" :key="index">
        <td style="width: 10%">
          <input
            type="checkbox"
            :name="tarefa.id"
            :id="tarefa.id"
            :checked="tarefa.concluida"
            @change="alteraStatus($event)"
          />
        </td>
        <td style="width: 90%">
          <label :for="tarefa.id">{{ tarefa.nome }}</label>
        </td>
        <td style="width: 10%">
          <button
            class="btn-remover"
            title="Remover"
            @click="remover(tarefa.id)"
          >
            X
          </button>
        </td>
      </tr>
    </table>
  </div>
  <p v-else><strong>Nenhuma tarefa adicionada!</strong></p>
</template>

<style scoped>
.titulo {
  margin: 40px 0 0 0;
  font-weight: 600;
}
table,
th,
td {
  width: 400px;
  border: 1px solid #b8b8b8;
  border-collapse: collapse;
  text-align: center;
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
  margin: 4px 5px;
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
