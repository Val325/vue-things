<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
      <nav>
        <RouterLink to="/">Tasklist</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
  </header>

  <RouterView />
</template>

<style scoped>
header{
  margin-left: auto;
  margin-right: auto;
  width: 6em  
}

a {
  margin: 5px;
}
</style>
