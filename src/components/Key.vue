<script setup>
const props = defineProps({
  text: String,
  isHalf: Boolean,
  isCommand: Boolean,
  isSubmit: Boolean,
});

const emits = defineEmits(['click']);
</script>

<template>
  <button
    @click="e => emits('click', e)"
    :class="{
      key: true,
      half: props.isHalf,
      command: props.isCommand,
      submit: props.isSubmit,
    }"
  >
    {{ props.text }}
  </button>
</template>

<style scoped>
.key {
  all: unset;
  background-color: white;
  border: 1px solid white;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 6.2vmin;
  height: 6.2vmin;
  backdrop-filter: blur(1.2vmin);
  border-radius: 16px;
  color: #38b9ff;
}

.half {
  height: 4vmin;
}

.command {
  background-color: #b2daff;
  font-weight: bolder;
}

.submit {
  background-color: #19acff;
  box-shadow: -9px 13px 23px rgba(0, 163, 255, 0.65),
    inset -3px 4px 11px #b0dfff;
  color: #b2daff;
}
</style>
