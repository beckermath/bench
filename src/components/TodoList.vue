<script>
import sampleTodos from "../data/todos.json";

export default {
  data() {
    return {
      todos: sampleTodos,
      newTodoTitle: "",
      filtered: false,
    };
  },
  methods: {
    addTodo() {
      const newTodo = {
        title: this.newTodoTitle,
        completed: false,
      };
      this.todos.push(newTodo);
    },
    removeTodo(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1);
    },
  },
  computed: {
    filteredTodos() {
      return this.todos.filter((todo) => !todo.completed);
    },
  },
};
</script>
<template>
  <h2>Todo List!</h2>
  <span>
    <input class="border" v-model="newTodoTitle" /><button
      @click="addTodo"
    >
      Add Todo
    </button>
    <input type="checkbox" v-model="filtered" />
    <span>Hide completed</span>
  </span>
  <div v-for="todo in filtered ? filteredTodos : todos">
    <span>
      <input v-model="todo.completed" type="checkbox" />
      <span>{{ todo.title }}</span>
      <button @click="removeTodo(todo)">Remove</button>
    </span>
  </div>
</template>
