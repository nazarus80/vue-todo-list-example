<template>
  <li>
    <span v-bind:class="{done: todo.completed}">
      <input type="checkbox" v-on:change="todo.completed = !todo.completed">
      <strong>{{ todo.id }}</strong>
      {{ todo.title | toUpper}}
    </span>
    <button
        class="rm"
        @click="$emit('remove-todo', todo.id)"
    >
      &times;
    </button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todo: Object,
    required: true
  },
  filters: {
    toUpper(value){
      return value.toUpperCase();
    }
  }
}
</script>

<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: .5rem 2rem;
  margin-bottom: 1rem;
}

.rm {
  background: red;
  color: #fff;
  border-radius: 50%;
  font-weight: bold;
}

input {
  margin-right: 1rem;
}


.done {
  text-decoration: line-through;
}
</style>