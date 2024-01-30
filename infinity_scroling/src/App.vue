<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <header>
    <h1>Infinity Scroling</h1>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
  margin-bottom: 40px;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    justify-content: center;
    place-items: center;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
