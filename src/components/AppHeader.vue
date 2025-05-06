<template>
  <header>
    <h1>Запомни слово</h1>

    <TotalScore value="100" />
  </header>
</template>

<script setup>
  import TotalScore from './TotalScore.vue'
</script>

<style>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
  }

  h1 {
    margin: 0;
    font-weight: 700;
    font-size: 16px;
    text-transform: uppercase;
    color: var(--default);
  }
</style>
