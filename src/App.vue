<script setup lang="ts">
import { ref, watch } from 'vue';

const I_AM_KEY = 'I_AM_KEY'

const team = [
  'Germano',
  'Henrique',
  'Matheus',
  'Douglas',
  'Fernando',
  'Vinicius',
]

const iAm = ref(localStorage.getItem(I_AM_KEY) || '')

watch([iAm], () => {
  localStorage.setItem(I_AM_KEY, iAm.value)
})

const reviewers = ref<string[]>([])

function randomMyReviewers() {
  const teamWithoutMe = team.filter(member => member.toUpperCase() !== iAm.value.toUpperCase())

  const shuffled = teamWithoutMe.sort(() => 0.5 - Math.random());

  reviewers.value = shuffled.slice(0, 2);
}
</script>

<template>
  <h1>Wellcome to random my reviewers</h1>

  <div>
    <p>The team is</p>
    <ul>
      <li v-for="member in team" :key="member">
        {{ member }}
      </li>
    </ul>
  </div>

  <form @submit.prevent="randomMyReviewers()">
    <p>I'm <input v-model="iAm" /> </p>
    <button type="submit">Random my reviewers</button>
  </form>

  <div>
    <p>Your reviewers are</p>
    <ul>
      <li v-for="member in reviewers" :key="member">
        {{ member }}
      </li>
    </ul>
  </div>

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
