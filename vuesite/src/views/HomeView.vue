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
      fetch('https://jsonplaceholder.typicode.com/posts?_limit=5')
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
    <div v-for="p in post" :key="p.id">
      <div class="post">
        <h2 class="idnum">{{ p.id }}</h2>
        <h2 class="title">{{ p.title }}</h2>
        <p>{{ p.body }}</p>
      </div>
    </div>
  </main>
</template>

<style>
main {
  text-align: center;
}
.post {
  border: 3px solid var(--color-border);
  margin: 20px;
  padding: 5px;
  border-radius: 12px;
}
.idnum {
  text-align: start;
  margin:10px;
}
</style>
