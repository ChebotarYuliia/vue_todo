<template>
  <div>
    <p>Completed Tasks: {{ todos.filter( todo => todo.done === true ).length }}</p>
    <p>Pending Tasks: {{ todos.filter( todo => todo.done === false ).length }}</p>
    <todo v-for="todo in todos" v-bind:todo="todo" v-bind:key="todo" v-on:delete-todo="deleteTodo"></todo>
  </div>
</template>
  

<script type = "text/javascript" >
import Todo from "./Todo.vue";
export default {
  props: ["todos"],
  components: {
    Todo
  },
  methods: {
    deleteTodo(todo) {
      const item = this.todos.indexOf(todo);
      this.todos.splice(item, 1);
    }
  }
};
</script>

<style>
</style>
