<script setup>
import TheWelcome from '../components/TheWelcome.vue'
import WelcomeItem from '../components/WelcomeItem.vue'
</script>

<script>
export default {
  data() {
    return {
      formInfo: {
        title: '',
        task: ''
      },
      post: []
    }
  },
  methods: {
    getPosts() {
      fetch('https://jsonplaceholder.typicode.com/posts?_limit=5')
        .then(response => response.json())
        .then(data => this.post = data)
    },
    sendPost(){
      // Simple POST request with a JSON body using fetch
      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          title: this.formInfo.title,
          task: this.formInfo.task 
        })
      };
      fetch("http://127.0.0.1:8000/", requestOptions)
        .then(response => response.json())
        .then(data => console.log(data))
    }
  },
  mounted() {
    this.getPosts()
  }
}


</script>

<template>
  <main>

    <div id="app">
      <form @submit.prevent="sendPost" method="post" action="http://127.0.0.1:8000/">
            <input type="title" v-model="formInfo.title" placeholder="Enter your title" name="title"><br><br>
            <textarea type="task" v-model="formInfo.task" placeholder="Enter your task" name="task"></textarea><br><br>
            <button type="submit">Submit task</button>
      </form>
    </div>

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
