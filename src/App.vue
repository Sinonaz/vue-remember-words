<script setup>
  import { ref } from 'vue'
  import AppButton from './components/AppButton.vue'
  import CardItem from './components/CardItem.vue'
  import TotalScore from './components/TotalScore.vue'

  const score = ref(0)
  const cards = ref([
    {
      word: 'carom',
      translation: '',
      state: 'closed',
      status: 'pending',
    },
  ])
</script>

<template>
  <main>
    <header>
      <h1>Запомни слово</h1>

      <TotalScore :value="score" />
    </header>

    <div class="cards">
      <CardItem
        :word="cards[0].word"
        :translation="cards[0].translation"
        :state="cards[0].state"
        :status="cards[0].status"
      />
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
