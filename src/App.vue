<template>
  <div id="app">
    <h2>RIA Todo List</h2>
    <hr>
    <form @submit.prevent="addItems">
      <input type="text" v-model="title">
      <button type="submit">Add</button>
    </form>
    <TodoList
      v-bind:todos="todos"
      @remove-item="removeItem"
      v-if="todos.length"
    />
    <p v-else-if>Items not found!</p>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
export default {
  name: 'App',
  components: {
    TodoList
  },
  data() {
    return {
      todos: [  ],
      title: ''
    }
  },
  methods: {
    removeItem(id){
      this.todos = this.todos.filter(t => t.id !== id);
    },
    addItems(){
      this.todos.push(
          {id: Date.now(), title: this.title, completed: false}
      );
      this.title = ''
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos/?_limit=3')
        .then(response => response.json())
        .then(json => {this.todos = json})
  }
}
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

form {
  display: flex;
}

input {
  width: 400px;
}
</style>
