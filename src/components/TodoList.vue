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
      this.newTodoTitle = "";
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
  <h2 class="p-5 text-xl font-bold text-center">Todo List</h2>
  <div class="flex items-center justify-center">
    <input
      class="w-1/4 p-1 border rounded-md"
      placeholder="What needs to be done?"
      v-model="newTodoTitle"
      @keyup.enter="addTodo"
    /><button
      class="w-1/6 p-1 m-4 text-white bg-blue-500 border rounded-md"
      @click="addTodo"
    >
      Add Todo
    </button>
    <input class="w-4 h-4 m-2" type="checkbox" v-model="filtered" />
    <span>Hide completed</span>
  </div>
  <div class="w-1/2 m-auto">
    <div v-for="todo in filtered ? filteredTodos : todos">
      <span>
        <input
          class="w-4 h-4 m-2"
          v-model="todo.completed"
          type="checkbox"
        />
        <span>{{ todo.title }}</span>
        <button
          class="w-20 m-2 text-white bg-red-500 border rounded-md"
          @click="removeTodo(todo)"
        >
          Remove
        </button>
      </span>
    </div>
  </div>
</template>
