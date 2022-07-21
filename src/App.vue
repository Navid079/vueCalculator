<script setup>
import { ref } from 'vue';
import Monitor from './components/Monitor.vue';
import Keyboard from './components/Keyboard.vue';

const history = ref('');
const operation = ref('');
const result = ref('');

const op1 = ref(0);
const op2 = ref(0);

function onOperandUpdate(operand) {
  op1.value = +operand;
  console.log(op1.value);
  operation.value = history.value + op1.value;
  if (operand.endsWith('.')) operation.value += '.0';
}
</script>

<template>
  <div class="calculator light">
    <Monitor :operation="operation" :result="result" />
    <Keyboard @operand-update="onOperandUpdate" />
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
