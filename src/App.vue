<script setup>
  import AppButton from './components/AppButton.vue'
  import AppHeader from './components/AppHeader.vue'
  import CardItem from './components/CardItem.vue'
</script>

<template>
  <main>
    <AppHeader />

    <div class="cards">
      <CardItem />
    </div>

    <AppButton class="main-btn"> Начать игру </AppButton>
  </main>
</template>

<style scoped>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 50px;
    padding: 60px;
  }

  .cards {
    flex-grow: 1;
    width: 100%;
  }

  .main-btn {
    display: block;
    width: fit-content;
    margin: 50px auto 0;
  }
</style>
