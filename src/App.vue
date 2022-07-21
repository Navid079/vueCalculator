<script setup>
import { ref } from 'vue';
import Monitor from './components/Monitor.vue';
import Keyboard from './components/Keyboard.vue';

const history = ref('');
const operation = ref('0');
const result = ref('');
const op = ref(0);

const darkMode = ref(false);

function operandUpdateHandler(operand, options) {
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

function operationHandler(operator) {
  if (operator === '%') {
    op.value /= 100;
  } else {
    history.value += op.value + operator;
    op.value = 0;
  }
  operation.value = history.value + op.value;
}

function calculateOneStep(operands, operators) {
  const op2 = operands.pop();
  const op1 = operands.pop();
  const operation = operators.pop();

  console.log(`calculating ${op1} ${operation} ${op2}`);

  switch (operation) {
    case '+':
      operands.push(op1 + op2);
      break;
    case '-':
      operands.push(op1 - op2);
      break;
    case '*':
      operands.push(op1 * op2);
      break;
    case '/':
      operands.push(op1 / op2);
      break;
  }
}

function submitHandler() {
  let number = '';
  const operandStack = [];
  const operatorStack = [];
  for (let letter of operation.value) {
    if ('0123456789.'.includes(letter)) number += letter;
    else {
      console.log(`Number ${+number} found! Pushing...`);
      console.log(`Operator ${letter} found!`);
      operandStack.push(+number);
      if (operatorStack.length > 0) {
        const lastOperator = operatorStack[operatorStack.length - 1];
        if ('+-'.includes(lastOperator) && '*/'.includes(letter)) {
          console.log(`New operator precedes!`);
        } else {
          console.log(`New operator doesn't precede. Calculating:`);
          calculateOneStep(operandStack, operatorStack);
        }
      }
      console.log('Pushing operator...');
      operatorStack.push(letter);
      number = '';
    }
  }
  operandStack.push(+number);
  while (operatorStack.length > 0)
    calculateOneStep(operandStack, operatorStack);

  let res = operandStack.pop();
  res = Math.round(res * 10000) / 10000;
  result.value = `=${res}`;
}

function modeChangeHandler() {
  darkMode.value = !darkMode.value;
}
</script>

<template>
  <div :class="{ page: 'true', dark: darkMode }">
    <div :class="{ calculator: true, dark: darkMode }">
      <Monitor :operation="operation" :result="result" :is-dark="darkMode" />
      <Keyboard
        @operand-update="operandUpdateHandler"
        @operation="operationHandler"
        @submit="submitHandler"
        @mode-change="modeChangeHandler"
        :is-dark="darkMode"
      />
    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.page {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #bbb;
  width: 100vw;
  height: 100vh;
}

.page.dark {
  background-color: #777;
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
  background-color: #f7f8fb;
  backdrop-filter: blur(102px);

  outline: 1rem solid black;
  overflow: hidden;
}

.calculator::before {
  content: '';
  color: white;
  display: block;
  width: 3rem;
  height: 3rem;
  background-color: black;
  border-bottom-left-radius: 100%;
  border-bottom-right-radius: 100%;
  position: absolute;
  top: -1rem;
}

.calculator.dark {
  background-color: #17181a;

  outline: 1rem solid goldenrod;
}

.calculator.dark::before {
  background-color: goldenrod;
}

</style>
