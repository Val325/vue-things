<script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<script>
export default {
  data() {
    return {
      post: []
    }
  },
  methods: {
    getPosts() {
      fetch('https://jsonplaceholder.typicode.com/posts/')
        .then(response => response.json())
        .then(data => this.post = data)
    }
  },
  mounted() {
    this.getPosts()
  }
}
  
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
    <div v-for="p in post" :key="p.id">
      <h2>{{ p.id }} - {{ p.title }}</h2>
      <p>{{ p.body }}</p>
    </div>
  </main>
</template>

<style>
main {
  text-align: center;
}
</style>
