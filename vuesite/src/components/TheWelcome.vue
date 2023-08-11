<script setup>
import WelcomeItem from './WelcomeItem.vue'
</script>

<template>
  <WelcomeItem>
    <template v-slot:header>
      <p>This is the header content</p>
    </template>
    <template v-slot:body>
      <p>This is the body content</p>
    </template>
    <template v-slot:footer>
      <p>This is the footer content</p>
    </template>
  </WelcomeItem>
</template>
