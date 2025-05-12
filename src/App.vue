<script setup>
  import { computed, onMounted, ref } from 'vue'
  import AppButton from './components/AppButton.vue'
  import CardItem from './components/CardItem.vue'
  import TotalScore from './components/TotalScore.vue'

  const score = ref(0)
  const cards = ref([])

  const modifiedCards = computed(() => {
    if (!cards.value.length) return []

    return cards.value.map((card) => {
      return {
        word: card.word,
        translation: card.translation,
        state: 'closed',
        status: 'pending',
      }
    })
  })

  async function fetchCards() {
    const response = await fetch('http://localhost:8080/api/random-words')

    if (!response.ok) return

    cards.value = await response.json()
  }

  onMounted(() => {
    fetchCards()
  })
</script>

<template>
  <main>
    <header>
      <h1>Запомни слово</h1>

      <TotalScore :value="score" />
    </header>

    <div class="cards">
      <CardItem
        v-for="card in modifiedCards"
        :key="card.word"
        :word="card.word"
        :translation="card.translation"
        :state="card.state"
        :status="card.status"
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
    counter-reset: count;
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
