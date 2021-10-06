<template>
  <div class="todolist">
    <h1>Todoアプリ</h1>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <a v-on:click="showTodo(todo)">{{ todo }}</a>
      </li>
    </ul>
    <button v-on:click="showTodo">＋</button>
    <div v-if="toggle">
      <Todo :value="{ oldTodo }" @addTodo="saveTodo" @delTodo="deleteTodo" />
    </div>
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
      oldTodo: "",
      toggle: true,
      todos: ["todo1", "todo2"],
    };
  },
  methods: {
    showTodo: function(todo = "") {
      this.toggle == true ? (this.toggle = false) : (this.toggle = true);
      if (typeof todo === "object") {
        this.oldTodo = "";
      } else {
        this.oldTodo = todo;
      }
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
