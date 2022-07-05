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
  <div class="flex items-center justify-center w-1/2 m-auto">
    <input
      class="w-full p-1 border border-gray-400 rounded-md"
      placeholder="What needs to be done?"
      v-model="newTodoTitle"
      @keyup.enter="addTodo"
    /><button
      class="w-1/2 p-1 m-4 text-white bg-blue-500 border rounded-md"
      @click="addTodo"
    >
      Add Todo
    </button>
  </div>
  <div class="w-1/2 m-auto mt-2">
    <div
      class="p-2 mt-1 mr-2 border-b rounded bg-slate-50 border-grey hover:bg-grey-lighter"
      v-for="todo in filtered ? filteredTodos : todos"
    >
      <input
        class="w-4 h-4 m-2"
        v-model="todo.completed"
        type="checkbox"
      />
      <input class="bg-slate-50" v-model="todo.title" />
      <button
        class="float-right w-20 h-8 text-white bg-red-500 border rounded-md"
        @click="removeTodo(todo)"
      >
        Remove
      </button>
    </div>
  </div>
  <div class="w-1/2 m-auto mt-2">
    <input class="w-4 h-4 m-2" type="checkbox" v-model="filtered" />
    <span>Hide completed</span>
  </div>
</template>
