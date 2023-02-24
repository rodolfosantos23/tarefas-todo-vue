<script>
export default {

  emits: ["tarefaAdicionada"],
  methods: {
    adicionarTarefa() {
      const tarefa = this.$refs.input.value;
      if (!tarefa) {
        alert("Digite a tarefa");
        return false;
      }

      this.$emit('tarefaAdicionada', {
        id: (new Date().getTime() + (1 + Math.random(0, 999)) * 0x10000) | 0,
        nome: this.$refs.input.value,
        concluida: false,
      });

      this.$refs.input.value = "";
      this.$refs.input.focus();
    },
  },
};
</script>

<template>
  <p><strong>Adicionar nova tarefa:</strong></p>
  <input type="text" ref="input" placeholder="Digite a tarefa" v-on:keyup.enter="adicionarTarefa" />
  <button @click="adicionarTarefa">Adicionar</button>
</template>

<style scoped>
p {
  margin: 5px;
}

input {
  width: 350px;
  height: 29px;
  border-radius: 10px;
  border: 1px solid #b4afaf;
  font-size: 14px;
  margin: 0px 0 15px 0px;
  padding: 5px 20px;
  color: #333;
  outline: none;
}

button {
  width: 140px;
  height: 34px;
  border: none;
  border-radius: 10px;
  color: #fff;
  font-size: 12px;
  font-weight: bold;
  cursor: pointer;
  background: #077a07;
  transition: all 0.3s;
}

button:hover {
  background: #099709;
}

button:active {
  background: #0cb60c;
}
</style>
