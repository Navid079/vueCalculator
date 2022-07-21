<script setup>
const props = defineProps({
  value: String,
});
</script>

<template>
  <div class="monitor">{{ props.value }}</div>
</template>

<style>
.monitor {
  background-color: aquamarine;
  width: 70%;
  height: 4rem;
  border-radius: 1.25rem;
  padding: 1rem;
  font-size: 3rem;
  text-align: right;
  user-select: none;
}
</style>
