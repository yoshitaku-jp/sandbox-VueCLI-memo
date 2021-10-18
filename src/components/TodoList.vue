<template>
  <div class="todolist">
    <h1>Todoアプリ</h1>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <a @click="showTodo(todo)">{{ todo.split("\n")[0] }}</a>
      </li>
    </ul>
    <button @click="showTodo">＋</button>
    <div v-if="isVisible">
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
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos")) || [];
  },
  data() {
    return {
      oldTodo: "",
      isVisible: false,
      todos: [],
    };
  },
  methods: {
    showTodo: function(todo = "") {
      this.isVisible = !this.isVisible
        ? (this.isVisible = false)
        : (this.isVisible = true);
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
      this.setTodos();
    },

    deleteTodo: function(targetTodo) {
      if (!targetTodo) {
        return;
      }
      this.todos = this.todos.filter((element) => element !== targetTodo);
      this.isVisible = false;
      this.setTodos();
    },
    setTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>
