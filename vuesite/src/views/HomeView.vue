<script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <main>
    <TheWelcome />
      <template slot="icon">
        icon
      </template>
      <template slot="heading">
        heading
      </template>
    <TheWelcome />
  </main>
</template>
