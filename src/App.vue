<script setup>
import { RouterLink, RouterView } from 'vue-router';
</script>

<template>
  <header>
    <nav class="flex flex-row justify-between items-center border border-l-neutral-600">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/register">Login</RouterLink>
    </nav>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  padding: 1rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
  font-size: large;
}

nav a {
  display: inline-block;
  border-left: 1px solid var(--color-border);
  font-size: large;
}

nav a:first-of-type {
  border: 0;
}
</style>
