<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <RouterView />
</template>

<style>
/* Global resets handled by Tailwind, minimal overrides here */
body {
  margin: 0;
  padding: 0;
  background-color: #f9f3e0; /* Fallback color matching tailwind config */
}
</style>