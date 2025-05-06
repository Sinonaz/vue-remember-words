<script setup>
  import { ref } from 'vue'
  import AppButton from './components/AppButton.vue'
  import CardItem from './components/CardItem.vue'
  import TotalScore from './components/TotalScore.vue'

  const score = ref(0)
  const cards = ref([
    {
      word: 'cat',
      translation: 'кошка',
      state: 'opened',
      status: 'success',
    },
    {
      word: 'dog',
      translation: 'собака',
      state: 'opened',
      status: 'success',
    },
    {
      word: 'tiger',
      translation: 'тигр',
      state: 'opened',
      status: 'fail',
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
        v-for="(card, index) in cards"
        :key="card.word"
        :number="index + 1"
        :word="card.word"
        :state="card.state"
        :status="card.status"
        :translation="card.translation"
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
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 50px 100px;
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
