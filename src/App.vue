<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.jpg" width="75" height="75" />
    <h2>Typing the World</h2>
  </header>
  <RouterView />
</template>

<style scoped>
header{
  text-align: center;
}
</style>
