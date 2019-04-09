<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" class="logo">
    <todo-list
      v-bind:todos="todos"
      @delete-from-todos="saveTodos"
      @edited-to-todos="saveTodos"
      @complite-todo="saveTodos"
      @return-in-todos="saveTodos"
    ></todo-list>
    <create-todo @create-todo="addTodo"></create-todo>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";
import CreateTodo from "./components/CreateTodo.vue";

export default {
  name: "app",
  components: {
    TodoList,
    CreateTodo
  },
  data() {
    return {
      todos: [
        {
          title: "Make plan for today",
          project: "Project A",
          done: false
        }
      ]
    };
  },
  mounted() {
    if (localStorage.getItem("todos")) {
      try {
        this.todos = JSON.parse(localStorage.getItem("todos"));
      } catch (e) {
        localStorage.removeItem("todos");
      }
    }
  },
  methods: {
    addTodo(todo) {
      this.todos.push(todo);
      this.saveTodos();
    },
    saveTodos() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem("todos", parsed);
    }
  }
};
</script>

<style>
.logo {
  margin: 10px auto;
  display: block;
}
</style>
