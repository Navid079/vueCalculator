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
  height: 10%;
  border-radius: 1.25rem;
  padding: 1rem;
  font-size: 4rem;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  user-select: none;
}
</style>
