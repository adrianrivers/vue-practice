<script setup>
import { reactive } from 'vue'
import ModalBody from './components/ModalBody.vue'

const state = reactive({
  header: 'I am a modal header',
  message: 'I am the modal message \u{1F984}',
})
</script>
<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
  </header>
  <p>Welcome</p>
  <main>
    <ModalBody buttonText="Show modal 1" :header="state.header" :message="state.message">
      <h1>I am Modal 1</h1>
      <p>Slots are cool</p>
      <template v-slot:links>
        <a href="/">I am a link</a>
        <a href="/">Hahahaha</a>
      </template>
    </ModalBody>
    <ModalBody buttonText="Show modal 2" :header="state.header" :message="state.message">
      <h1>I am Modal 2</h1>
      <template v-slot:links>
        <a href="/">Hahahaha</a>
      </template>
    </ModalBody>
  </main>
</template>

<style>
@import './assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
