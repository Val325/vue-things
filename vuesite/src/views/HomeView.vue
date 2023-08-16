<script setup>
import TheWelcome from '../components/TheWelcome.vue'
import WelcomeItem from '../components/WelcomeItem.vue'
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

/*
<div class="post">
          <h2 class="idnum">{{ p.id }}</h2>
          <h2 class="title">{{ p.title }}</h2>
          <p>{{ p.body }}</p>
        </div>
*/
</script>

<template>
  <main>
    <div v-for="p in post" :key="p.id">
      <Transition name="slide-fade" appear>
        <WelcomeItem>
          <template v-slot:id>
            <h2 class="idnum">{{ p.id }}</h2>
          </template>
          <template v-slot:title>
            <h2 class="title">{{ p.title }}</h2>
          </template>
          <template v-slot:body>
            <p>{{ p.body }}</p>
          </template>
        </WelcomeItem>
      </Transition>
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
.slide-fade-enter-active {
  transition: all 1s ease-out;
}

.slide-fade-leave-active {
  transition: all 1s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(100px);
  opacity: 1;
}
</style>
