<script setup>
import TheWelcome from '../components/TheWelcome.vue'
import WelcomeItem from '../components/WelcomeItem.vue'
</script>

<script>
//https://jsonplaceholder.typicode.com/posts?_limit=5
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
      fetch('http://127.0.0.1:8000/api/posts')
        .then(response => response.json())
        .then(data => this.post = data)
    },
    sendPost(){
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
      location.reload();
    },
    deletePost(id){
      const requestOptions = {
        method: "DELETE",
      };
      fetch("http://127.0.0.1:8000/posts/" + id, requestOptions)
        .then(response => response.json())
        .then(data => console.log(data))
      location.reload();
    },
    changePost(){
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
          <div>
            <input type="title" v-model="formInfo.title" placeholder="Enter your title" name="title"><br><br>
            <textarea type="task" v-model="formInfo.task" placeholder="Enter your task" name="task"></textarea><br><br>
            <button class="button-37" type="submit">Submit task</button>
          </div>
      </form>
    </div>

    <div v-for="p in post" :key="p.id">
      <Transition name="slide-fade" appear>
        <div>
          <WelcomeItem>
            <template v-slot:id>
              <h2 class="idnum">{{ p.id }}</h2>
            </template>
            <template v-slot:title>
              <h2 class="title">{{ p.title }}</h2>
            </template>
            <template v-slot:body>
              <p>{{ p.task }}</p>
            </template>
          </WelcomeItem>
          <input @click=deletePost(p.id) type="button" class="button-37" value="Task completed" >
        </div>
        
      </Transition>
    </div>
  </main>
</template>

<style>
main {
  text-align: center;
}
form > div{
  margin-left: auto;
  margin-right: auto;
  width:370px;
}



/* CSS */
.button-37 {
  height: 50px;
  background-color: #13aa52;
  border: 1px solid #13aa52;
  border-radius: 4px;
  box-shadow: rgba(0, 0, 0, .1) 0 2px 4px 0;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  font-family: "Akzidenz Grotesk BQ Medium", -apple-system, BlinkMacSystemFont, sans-serif;
  font-size: 16px;
  font-weight: 400;
  outline: none;
  outline: 0;
  padding: 10px 25px;
  text-align: center;
  transform: translateY(0);
  transition: transform 150ms, box-shadow 150ms;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button-37:hover {
  box-shadow: rgba(0, 0, 0, .15) 0 3px 9px 0;
  transform: translateY(-2px);
}

@media (min-width: 768px) {
  .button-37 {
    padding: 10px 30px;
  }
}

input {
  width: 400px;
  height: 10px;
  padding: 12px 20px;
  box-sizing: border-box;
  border: 2px solid #ccc;
  border-radius: 4px;
  background-color: #f8f8f8;
  font-size: 16px;
  resize: none;  
}
textarea {
  width: 400px;
  height: 150px;
  padding: 12px 20px;
  box-sizing: border-box;
  border: 2px solid #ccc;
  border-radius: 4px;
  background-color: #f8f8f8;
  font-size: 16px;
  resize: none;
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
