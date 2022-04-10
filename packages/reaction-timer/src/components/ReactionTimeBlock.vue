<script setup lang="ts">
import { ref, onUpdated, onMounted, onUnmounted, defineEmits } from 'vue'

interface BlockProps {
  delay: null | number
}

interface BlockEmit {
  (event: 'end', reactionTime: number): void
}

const props = defineProps<BlockProps>()
const emit = defineEmits<BlockEmit>()

const showBlock = ref<boolean>(false)
const timer = ref(0)
const reactionTime = ref<number>(0)

const startTimer = () => {
  timer.value = setInterval(() => {
    reactionTime.value += 10
  }, 10)
}

const stopTimer = () => {
  clearInterval(timer.value)
  emit('end', reactionTime.value)
}

onMounted(() => {
  if (props.delay)
    setTimeout(() => {
      showBlock.value = true
      startTimer()
    }, props.delay)
})

onUpdated(() => {
  console.log('Component updated')
})

onUnmounted(() => {
  console.log('Component unmounted')
})
</script>

<template>
  <div class="block" v-if="showBlock" @click="stopTimer">Click me ⚠️</div>
</template>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background-color: var(--vt-c-green);
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>
