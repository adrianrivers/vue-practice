<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header
    class="flex flex-col w-full px-6 py-4 text-center bg-white shadow sm:flex-row sm:text-left sm:justify-between sm:items-baseline"
  >
    <div>
      <a href="/" class="text-2xl no-underline text-grey-darkest hover:text-blue-dark">🏠</a>
    </div>
    <div class="wrapper">
      <nav>
        <RouterLink
          to="/about"
          class="p-2 text-white transition ease-in-out bg-green-500 rounded-full hover:bg-green-600 active:bg-violet-700 focus:outline-none"
        >
          About
        </RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style>
@import '@/assets/base.css';
</style>
