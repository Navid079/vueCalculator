<script setup>
import { ref } from 'vue';
import Monitor from './components/Monitor.vue';
import Keyboard from './components/Keyboard.vue';

const result = ref(0);
</script>

<template>
  <div class="calculator light">
    <Monitor :value="result" />
    <Keyboard />
  </div>
</template>

<style>
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
  width: 37.5vmin;
  height: 81.2vmin;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

.calculator.light {
  background-color: #F7F8FB;
  backdrop-filter: 102px;
  border-radius: 40px;
}
</style>
