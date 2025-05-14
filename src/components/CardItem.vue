<template>
  <div
    class="card"
    @click.once="isOpened = true"
    :style="{ cursor: answerStatus !== 'pending' ? 'default' : 'pointer' }"
  >
    <span class="card__number"></span>

    <div class="card__result">
      <IconSuccess v-if="answerStatus === 'success'" width="40" height="40" />
      <IconFail v-if="answerStatus === 'fail'" width="40" height="40" />
    </div>

    <p class="card__word">{{ !isOpened ? word : translation }}</p>

    <p v-if="answerStatus === 'pending' && !isOpened" class="card__label">Перевернуть</p>

    <div v-if="isOpened" class="card__btns">
      <button class="btn-fail" @click="answer('fail')">
        <IconFail />
      </button>
      <button class="btn-success" @click="answer('success')">
        <IconSuccess />
      </button>
    </div>
  </div>
</template>

<script setup>
  import IconFail from './Icons/IconFail.vue'
  import IconSuccess from './Icons/IconSuccess.vue'
  import { inject, ref } from 'vue'
  import { scoreProvide } from '@/constants.js'

  const { word, translation, state, status } = defineProps({
    word: String,
    translation: String,
    state: {
      type: String,
      validator(value) {
        return ['closed', 'opened'].includes(value)
      },
    },
    status: {
      type: String,
      validator(value) {
        return ['success', 'fail', 'pending'].includes(value)
      },
    },
  })

  const isOpened = ref(state === 'opened')
  const answerStatus = ref(status)

  const score = inject(scoreProvide)

  function answer(status) {
    answerStatus.value = status
    isOpened.value = false

    updateScore(status === 'success')
  }

  function updateScore(isCorrect) {
    if (score.value <= 0 && !isCorrect) {
      return
    }

    if (isCorrect) {
      score.value = score.value + 10
    } else {
      score.value = score.value - 4
    }
  }
</script>

<style>
  .card {
    position: relative;
    z-index: 1;
    display: grid;
    grid-template-rows: min-content 1fr min-content;
    min-height: 375px;
    padding: 20px;
    background: white;
    border-radius: 16px;
    box-shadow: 0px 0px 16px 0px #0000001a;
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

  .card__result {
    position: absolute;
    top: 10px;
    left: 50%;
    transform: translateX(-50%);
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
    counter-increment: count;
  }

  .card__number::before {
    content: counter(count, decimal-leading-zero);
  }

  .btn-success,
  .btn-fail {
    border: none;
    padding: 0;
    background: none;
    cursor: pointer;
  }

  .card__btns {
    display: flex;
    align-items: center;
    gap: 32px;
    justify-self: center;
    width: fit-content;
    margin-bottom: -5px;
    padding: 0 10px;
    background: white;
  }
</style>
