<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  buttonText: { type: String, required: true, default: 'Show modal' },
  header: { type: String, required: true },
  message: { type: String, required: true },
  isDark: { type: Boolean, required: false, default: false },
})

const isOpen = ref(false)

const handleShowModal = () => {
  console.log()
  isOpen.value = !isOpen.value
}

const determineTheme = computed(() => (props.isDark ? 'dark' : 'light'))
</script>

<template>
  <button @click="handleShowModal()">{{ buttonText }}</button>
  <Teleport to="body">
    <Transition>
      <div v-if="isOpen" class="backdrop" @click.self="handleShowModal()">
        <div class="modal" :class="determineTheme">
          <h1>{{ header }}</h1>
          <p>{{ message }}</p>
          <slot>This will show if no content has been passed into the slot</slot>
          <div class="actions">
            <slot name="links"></slot>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.modal {
  width: 400px;
  padding: 20px;
  margin: 100px auto;
  border-radius: 10px;
  color: black;
}

.modal.dark {
  background-color: black;
  color: white;
}

.modal.dark p {
  color: white;
}

.modal.light {
  background-color: white;
}

.backdrop {
  top: 0;
  left: 0;
  position: fixed;
  background-color: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}

h1 {
  color: green;
  border: none;
  padding: 0;
}

p {
  color: var(--color-text-dark);
}

.actions {
  text-align: center;
  padding: 1em;
  border-radius: 3px;
}
</style>
