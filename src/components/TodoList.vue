<template>
  <div>
    <div class="todo__info">
      <p>Completed Tasks: {{ todos.filter( todo => todo.done === true ).length }}</p>
      <p>Pending Tasks: {{ todos.filter( todo => todo.done === false ).length }}</p>
    </div>
    <div class="todo__list">
      <div class="doubling ui four cards">
        <todo
          v-for="todo in todos"
          v-bind:todo="todo"
          v-bind:key="todo"
          v-on:delete-todo="deleteTodo"
          v-on:complete-todo="completeTodo"
          v-on:return-in-todo="returnTodo"
        ></todo>
      </div>
    </div>
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
    },
    completeTodo(todo) {
      const item = this.todos.indexOf(todo);
      this.todos[item].done = true;
    },
    returnTodo(todo) {
      const item = this.todos.indexOf(todo);
      this.todos[item].done = false;
    }
  }
};
</script>

<style>
.todo__info {
  padding: 15px;
  background: #fcb637;
  color: #fff;
}
.todo__info p {
  margin: 0;
  font-size: 14px;
}
.todo__info p span {
  font-size: 16px;
  font-weight: bold;
}
.todo__list {
  padding: 15px;
}
</style>
