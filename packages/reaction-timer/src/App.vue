<script setup lang="ts">
import { reactive } from 'vue'
import ReactionTimeBlock from './components/ReactionTimeBlock.vue'
import ReactTimeResult from './components/ReactionTimeResult.vue'

interface State {
  isPlaying: boolean
  delay: null | number
  score: number
  showResults: boolean
}

const state: State = reactive({
  isPlaying: false,
  delay: null,
  score: 0,
  showResults: false,
})

const startGame = () => {
  state.delay = 2000 + Math.random() * 5000 // Between 2 and 7 seconds
  state.isPlaying = true
  state.showResults = false
}

const endGame = (reactionTime: number) => {
  state.isPlaying = false
  state.score = reactionTime
  state.showResults = true
}
</script>

<template>
  <div class="controls">
    <h1>Reaction Timer</h1>
    <button @click="startGame" :disabled="state.isPlaying">Play</button>
  </div>
  <ReactionTimeBlock v-if="state.isPlaying" :delay="state.delay" @end="endGame" />
  <Transition>
    <ReactTimeResult v-if="state.showResults" :score="state.score" />
  </Transition>
</template>

<style>
@import './assets/base.css';

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

#app {
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;

  display: flex;
  flex-direction: column;
  justify-content: center;
}

.controls {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.controls button {
  background-color: var(--vt-c-green);
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 1rem;
  letter-spacing: 0.1rem;
  cursor: pointer;
  margin: 10px;
  text-transform: uppercase;
  font-weight: bold;
}

.controls button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
