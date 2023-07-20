<script setup>
import { reactive } from 'vue'

const state = reactive({
  operation: 'add',
  number1: '',
  number2: '',
  result: 'Insira dois números'
})

function calculate() {
  const { operation, number1, number2 } = state

  switch (operation) {
    case 'add':
      state.result = number1 + number2
      break
    case 'subtract':
      state.result = number1 - number2
      break
    case 'multiply':
      state.result = number1 * number2
      break
    case 'divide':
      state.result = number1 / number2
      break
    default:
      state.result = 0
      break
  }

  switch ((number1, number2)) {
    case '':
      state.result = 'Insira dois números'
      break
    default:
      break
  }
}
</script>

<template>
  <div class="container">
    <div class="row mt-4">
      <header class="text-center p-4 bg-dark text-white">
        <h1>Calculadora Aritimética</h1>
      </header>
    </div>

    <div class="row mt-5">
      <form>
        <input class="form-control" type="number" v-model="state.number1" @input="calculate" />
        <div>
          <span class="fs-3 fw-bold" v-if="state.operation === 'add'">+</span>
          <span class="fs-3 fw-bold" v-else-if="state.operation === 'subtract'">-</span>
          <span class="fs-3 fw-bold" v-else-if="state.operation === 'multiply'">*</span>
          <span class="fs-3 fw-bold" v-else>/</span>
        </div>
        <input class="form-control" type="number" v-model="state.number2" @input="calculate" />
        <select
          class="form-select shadow-none d-inline bg-light"
          v-model="state.operation"
          @change="calculate"
        >
          <option value="add">Adição</option>
          <option value="subtract">Subtração</option>
          <option value="multiply">Multiplicação</option>
          <option value="divide">Divisão</option>
        </select>
      </form>
    </div>

    <div class="mt-5 text-center bg-light p-5">
      <span class="fs-2">{{ state.result }}</span>
    </div>
  </div>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 12px;
}
input,
select {
  font-family: 'Poppins', sans-serif;
  border: 2px solid gray;
  border-radius: 4px;
  text-align: center;
}

select,
option {
  cursor: pointer;
}

input:focus,
select:focus {
  border-color: black;
  box-shadow: none;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
</style>
