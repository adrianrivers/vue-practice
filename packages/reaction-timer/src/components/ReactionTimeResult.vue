<script setup lang="ts">
interface ReactionTimeResultProps {
  score: number
}

defineProps<ReactionTimeResultProps>()

const determineRank = (score: number) => {
  if (score < 250) {
    return 'Sick m8!'
  } else if (score < 400) {
    return 'Holy cow!'
  } else {
    return 'You should be ashamed of yourself!'
  }
}
</script>

<template>
  <div class="result">
    <p>Reaction time {{ score }}ms</p>
    <p class="rank">{{ determineRank(score) }}</p>
  </div>
</template>

<style scoped>
.result {
  padding-top: 3em;
  margin: 0 auto;
  text-align: center;
}
.rank {
  font-size: 1.5rem;
  font-weight: bold;
  color: var(--vt-c-green);
}
</style>
