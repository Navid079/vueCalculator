<script setup>
import Key from './Key.vue';
</script>

<template>
  <div class="keyboard">
    <div class="keyboard-row">
      <Key :is-half="true" text="MC" />
      <Key :is-half="true" text="M-" />
      <Key :is-half="true" text="M+" />
      <Key :is-half="true" text="M" />
    </div>
    <div class="keyboard-row">
      <Key text="AC" />
      <Key text="<-" />
      <Key text="/" :is-command="true" />
      <Key text="*" :is-command="true" />
    </div>
    <div class="keyboard-row">
      <Key text="7" />
      <Key text="8" />
      <Key text="9" />
      <Key text="-" :is-command="true" />
    </div>
    <div class="keyboard-row">
      <Key text="4" />
      <Key text="5" />
      <Key text="6" />
      <Key text="+" :is-command="true" />
    </div>
    <div class="keyboard-row">
      <Key text="1" />
      <Key text="2" />
      <Key text="3" />
      <Key text="%" :is-command="true" />
    </div>
    <div class="keyboard-row">
      <Key text="0" />
      <Key text="." />
      <Key text="^" :is-command="true" />
      <Key text="=" :is-submit="true" />
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
