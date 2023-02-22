<script>
export default {
  props: {
    porcentagem: Number,
  },
  computed: {
    estiloBarra() {
      return {
        width: `${this.porcentagem}%`,
      };
    },
  },
};
</script>

<template>
  <div class="porcentagem">
    <div class="barra" :style="estiloBarra">
      <span>{{ porcentagem.toFixed(2) }} %</span>
    </div>
  </div>
</template>

<style scoped>
.porcentagem {
  width: 400px;
  height: 26px;
  border: 1px solid #333;
  text-align: center;
  margin: 0 0 35px 0;
  display: flex;
}

.porcentagem .barra {
  height: 100%;
  background: #0ad40a;
  transition: all 0.5s;
}

.porcentagem .barra span {
  display: block;
  width: 400px;
}
</style>
