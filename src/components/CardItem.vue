<template>
  <div class="card" @click="emit('flip')">
    <span class="card__number">06</span>

    <p class="card__word">dust-coat</p>

    <p class="card__label">Перевернуть</p>
  </div>
</template>

<script setup>
  const emit = defineEmits(['flip', 'update:status'])
</script>

<style>
  .card {
    position: relative;
    z-index: 1;
    display: grid;
    grid-template-rows: min-content 1fr min-content;
    max-width: 250px;
    min-height: 375px;
    padding: 20px;
    background: white;
    border-radius: 16px;
    box-shadow: 0px 0px 16px 0px #0000001a;
    cursor: pointer;
    transition: box-shadow 0.2s;

    &::before {
      content: '';
      position: absolute;
      z-index: -1;
      inset: 28px 20px;
      border: 1px solid #cce8ff;
      border-radius: 12px;
    }

    &:hover {
      box-shadow: 10px 10px 10px 0px #0000000d;
    }
  }

  .card__label {
    justify-self: center;
    margin: 0;
    padding: 0 5px;
    font-weight: 700;
    font-size: 12px;
    text-transform: uppercase;
    background: white;
  }

  .card__word {
    margin: 0;
    justify-self: center;
    align-self: center;
    font-size: 18px;
    text-align: center;
  }

  .card__number {
    justify-self: start;
    margin-left: 10px;
    padding: 0 5px;
    font-size: 14px;
    background: white;
  }
</style>
