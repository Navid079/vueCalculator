<script setup>
import { ref } from 'vue';
import Monitor from './components/Monitor.vue';

const result = ref(0);
</script>

<template>
  <Monitor :value="result" />
</template>

<style scoped></style>
