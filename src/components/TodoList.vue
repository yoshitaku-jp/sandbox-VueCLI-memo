<template>
  <div class="todolist">
    <h1>Todoアプリ</h1>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <span>{{ todo }}</span>
      </li>
    </ul>
    <button v-on:click="showTodo">＋</button>
    <div v-if="toggle"><Todo @addTodo="saveTodo" @delTodo="deleteTodo" /></div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";

export default {
  name: "TodoList",
  components: {
    Todo,
  },
  data: function() {
    return {
      newItem: "",
      toggle: true,
      todos: ["todo1", "todo2"],
    };
  },
  methods: {
    showTodo: function() {
      this.toggle == true ? (this.toggle = false) : (this.toggle = true);
    },

    saveTodo: function(newTodo) {
      if (!newTodo) {
        return;
      }
      this.todos.push(newTodo);
    },

    deleteTodo: function(targetTodo) {
      console.log(targetTodo);
      if (!targetTodo) {
        return;
      }
      this.todos = this.todos.filter((element) => element !== targetTodo);
    },
  },
};
</script>
