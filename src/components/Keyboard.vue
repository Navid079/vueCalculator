<script setup>
import { ref } from 'vue';
import Key from './Key.vue';

const props = defineProps({ isDark: Boolean });

const emit = defineEmits([
  'operation',
  'submit',
  'operandUpdate',
  'modeChange',
]);

const operand = ref('0');
const memory = ref(0);
const modeKey = ref(null)
const mode = ref('D')

function handleNumKeys(num) {
  if (num === 'AC') {
    operand.value = '';
    return emit('operandUpdate', operand.value, { reset: true });
  }
  if (num === '<-' && operand.value !== '') {
    operand.value = operand.value.slice(0, -1);
    return emit('operandUpdate', operand.value);
  } else if (num === '<-') return;
  if (num === '.' && operand.value.includes('.')) return;
  operand.value += num;
  emit('operandUpdate', operand.value);
}

function handleOperatorKeys(operator) {
  emit('operation', operator);
  operand.value = '';
}

function handleMode() {
  mode.value = mode.value === 'D' ? 'L' : 'D';
  emit('modeChange');
}
</script>

<template>
  <div class="keyboard">
    <div class="keyboard-row">
      <Key
        :is-dark="props.isDark"
        :is-half="true"
        text="MC"
        @click="() => (memory = 0)"
      />
      <Key
        :is-dark="props.isDark"
        :is-half="true"
        text="M-"
        @click="() => (memory -= operand)"
      />
      <Key
        :is-dark="props.isDark"
        :is-half="true"
        text="M+"
        @click="() => (memory += operand)"
      />
      <Key
        :is-dark="props.isDark"
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
      <Key :is-dark="props.isDark" text="AC" @click="handleNumKeys" />
      <Key :is-dark="props.isDark" text="<-" @click="handleNumKeys" />
      <Key
        :is-dark="props.isDark"
        text="/"
        :is-command="true"
        @click="handleOperatorKeys"
      />
      <Key
        :is-dark="props.isDark"
        text="*"
        :is-command="true"
        @click="handleOperatorKeys"
      />
    </div>
    <div class="keyboard-row">
      <Key :is-dark="props.isDark" text="7" @click="handleNumKeys" />
      <Key :is-dark="props.isDark" text="8" @click="handleNumKeys" />
      <Key :is-dark="props.isDark" text="9" @click="handleNumKeys" />
      <Key
        :is-dark="props.isDark"
        text="-"
        :is-command="true"
        @click="handleOperatorKeys"
      />
    </div>
    <div class="keyboard-row">
      <Key :is-dark="props.isDark" text="4" @click="handleNumKeys" />
      <Key :is-dark="props.isDark" text="5" @click="handleNumKeys" />
      <Key :is-dark="props.isDark" text="6" @click="handleNumKeys" />
      <Key
        :is-dark="props.isDark"
        text="+"
        :is-command="true"
        @click="handleOperatorKeys"
      />
    </div>
    <div class="keyboard-row">
      <Key :is-dark="props.isDark" text="1" @click="handleNumKeys" />
      <Key :is-dark="props.isDark" text="2" @click="handleNumKeys" />
      <Key :is-dark="props.isDark" text="3" @click="handleNumKeys" />
      <Key
        :is-dark="props.isDark"
        text="%"
        :is-command="true"
        @click="handleOperatorKeys"
      />
    </div>
    <div class="keyboard-row">
      <Key :is-dark="props.isDark" text="0" @click="handleNumKeys" />
      <Key :is-dark="props.isDark" text="." @click="handleNumKeys" />
      <Key
        :is-dark="props.isDark"
        ref="modeKey"
        :text="mode"
        :is-command="true"
        @click="handleMode"
      />
      <Key
        :is-dark="props.isDark"
        text="="
        :is-submit="true"
        @click="() => emit('submit')"
      />
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
