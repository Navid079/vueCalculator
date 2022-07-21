<script setup>
import { ref } from 'vue';
import Monitor from './components/Monitor.vue';
import Keyboard from './components/Keyboard.vue';

const history = ref('');
const operation = ref('0');
const result = ref('');

const op = ref(0);

function onOperandUpdate(operand, options) {
  op.value = +operand || 0;
  if (options && options.reset) {
    history.value = '';
    operation.value = '0';
    result.value = '';
    op.value = 0;
  }
  operation.value = history.value + op.value;
  if (operand.endsWith('.')) operation.value += '.0';
}

function onOperation(operator) {
  history.value += op.value + operator;
  op.value = 0;
  operation.value = history.value + op.value;
}
</script>

<template>
  <div class="calculator light">
    <Monitor :operation="operation" :result="result" />
    <Keyboard @operand-update="onOperandUpdate" @operation="onOperation" />
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: black;
  width: 100vw;
  height: 100vh;
}

.calculator {
  font-family: 'Poppins';
  width: 37.5vmin;
  height: 81.2vmin;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  border-radius: 40px;
}

.calculator.light {
  background-color: #f7f8fb;
  backdrop-filter: blur(102px);
}
</style>
