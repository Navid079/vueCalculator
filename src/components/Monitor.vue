<script setup>
const props = defineProps({
  operation: String,
  result: String,
  isDark: Boolean,
});
</script>

<template>
  <div class="monitor">
    <div class="operation-container scrollbar">
      {{ props.operation }}
    </div>
    <div :class="{ 'result-container': true, dark: isDark, scrollbar: true }">
      {{ props.result }}
    </div>
  </div>
</template>

<style>
.monitor {
  height: 23vmin;
  width: 100%;
  font-size: 3rem;
  padding: 10.2vmin 1rem 0 1rem;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  user-select: none;
  text-align: right;
}

.operation-container {
  height: 3.6vmin;
  font-size: 3.3vmin;
  line-height: 3.5vmin;
  color: #818181;
}

.result-container {
  height: 7.2vmin;
  font-size: 6.5vmin;
  line-height: 6.8vmin;
  color: #424242;
  overflow-x: scroll;
}

.result-container.dark {
  color: white;
}

.scrollbar::-webkit-scrollbar {
  display: none;
}

.scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style>
