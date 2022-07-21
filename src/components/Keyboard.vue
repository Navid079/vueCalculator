<script setup>
import { ref } from 'vue';
import Key from './Key.vue';

const emit = defineEmits(['operation', 'submit', 'operandUpdate']);

const operand = ref('');
const memory = ref(0);

function handleNumKeys(num) {
  if (operand.value !== '') {
    if (num === '<-') {
      operand.value = operand.value.slice(0, -1);
      return emit('operandUpdate', operand.value, { reset: true });
    }
    if (num === 'AC') {
      operand.value = '';
      return emit('operandUpdate', operand.value, { reset: true });
    }
  }
  if (num === '.' && operand.value.includes('.')) return;
  operand.value += num;
  emit('operandUpdate', operand.value);
}

function handleOperatorKeys(num) {
  emit('operation', num);
  operand = '';
}
</script>

<template>
  <div class="keyboard">
    <div class="keyboard-row">
      <Key :is-half="true" text="MC" @click="() => (memory = 0)" />
      <Key :is-half="true" text="M-" @click="() => (memory -= operand)" />
      <Key :is-half="true" text="M+" @click="() => (memory += operand)" />
      <Key
        :is-half="true"
        text="M"
        @click="
          () => {
            operand = memory.toString();
            emit('operandUpdate', operand);
          }
        "
      />
    </div>
    <div class="keyboard-row">
      <Key text="AC" @click="handleNumKeys" />
      <Key text="<-" @click="handleNumKeys" />
      <Key text="/" :is-command="true" @click="handleOperatorKeys" />
      <Key text="*" :is-command="true" @click="handleOperatorKeys" />
    </div>
    <div class="keyboard-row">
      <Key text="7" @click="handleNumKeys" />
      <Key text="8" @click="handleNumKeys" />
      <Key text="9" @click="handleNumKeys" />
      <Key text="-" :is-command="true" @click="handleOperatorKeys" />
    </div>
    <div class="keyboard-row">
      <Key text="4" @click="handleNumKeys" />
      <Key text="5" @click="handleNumKeys" />
      <Key text="6" @click="handleNumKeys" />
      <Key text="+" :is-command="true" @click="handleOperatorKeys" />
    </div>
    <div class="keyboard-row">
      <Key text="1" @click="handleNumKeys" />
      <Key text="2" @click="handleNumKeys" />
      <Key text="3" @click="handleNumKeys" />
      <Key text="%" :is-command="true" @click="handleOperatorKeys" />
    </div>
    <div class="keyboard-row">
      <Key text="0" @click="handleNumKeys" />
      <Key text="." @click="handleNumKeys" />
      <Key text="^" :is-command="true" @click="handleOperatorKeys" />
      <Key text="=" :is-submit="true" @click="() => emit('submit')" />
    </div>
  </div>
</template>

<style>
.keyboard {
  width: 100%;
  height: 58.2vmin;
}

.keyboard-row {
  display: flex;
  width: 100%;
  padding: 1rem;
  justify-content: space-around;
}
</style>
