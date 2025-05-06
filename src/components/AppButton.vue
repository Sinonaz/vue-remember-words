<template>
  <button class="button" type="button">
    <slot />
  </button>
</template>

<script setup></script>

<style scoped>
  .button {
    min-width: 335px;
    padding: 16px;
    background: var(--c-primary);
    font-size: 24px;
    line-height: 1;
    font-family: var(--font);
    color: white;
    border: none;
    border-radius: 100px;
    cursor: pointer;
  }
</style>
