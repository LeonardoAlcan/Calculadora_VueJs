<script setup>
import { ref, computed } from 'vue';

const numero1 = ref(0);
const numero2 = ref(0);
const operacao = ref('+');

const resultado = computed(() => {
  switch (operacao.value) {
    case '+':
      return numero1.value + numero2.value;
    case '-':
      return numero1.value - numero2.value;
    case '*':
      return numero1.value * numero2.value;
    case '/':
      return numero2.value !== 0 ? numero1.value / numero2.value : 'Erro (divisão por zero)';
    default:
      return 'Operação inválida';
  }
});

</script>

<template>
  <div class="calculator">
    <h1>Calculadora Aritmética</h1>

    <div class="inputs">
      <input type="number" v-model.number="numero1" placeholder="Número 1">
      <select v-model="operacao">
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">*</option>
        <option value="/">/</option>
      </select>
      <input type="number" v-model.number="numero2" placeholder="Número 2">
    </div>

    <div class="resultado">
      <h2>Resultado: {{ resultado }}</h2>
    </div>
  </div>
</template>

<style scoped>
.calculator {
  max-width: 400px;
  margin: auto;
  padding: 2rem;
  font-family: sans-serif;
  text-align: center;
}

.inputs {
  display: flex;
  justify-content: space-between;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

input, select {
  flex: 1;
  padding: 0.5rem;
  font-size: 1rem;
}
</style>
