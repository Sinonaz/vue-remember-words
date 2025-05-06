<template>
  <div class="score">
    <span>{{ value }}</span>
    <IconHeart />
  </div>
</template>

<script setup>
  import IconHeart from './Icons/IconHeart.vue'

  defineProps({
    value: {
      type: Number,
      default: 0,
    },
  })
</script>

<style>
  .score {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px;
    font-weight: 700;
    font-size: 16px;
    line-height: 1;
    color: var(--c-primary);
    border-radius: 36px;
    background: #cce8ff;
    box-shadow: 0px 0px 4px 0px #00000026;
  }
</style>
