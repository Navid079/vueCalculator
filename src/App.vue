<script setup>
import { ref } from 'vue';
import Monitor from './components/Monitor.vue';
import Keyboard from './components/Keyboard.vue';

const operation = ref('6000/2+3227*2')
const result = ref("=12,454");
</script>

<template>
  <div class="calculator light">
    <Monitor :operation="operation" :result="result" />
    <Keyboard />
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
  background-color: #F7F8FB;
  backdrop-filter: blur(102px);
}
</style>
