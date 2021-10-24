<template>
  <div class="todolist">
    <h1>Todoアプリ</h1>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <a @click="showTodo(todo, index)">{{ todo.split("\n")[0] }}</a>
      </li>
    </ul>
    <button @click="showTodo">＋</button>
    <div v-if="isVisible">
      <TodoItem
        :value="{ oldTodo, index }"
        @addTodo="saveTodo"
        @delTodo="deleteTodo"
      />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "TodoList",
  components: {
    TodoItem,
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos")) || [];
  },
  data() {
    return {
      oldTodo: "",
      isVisible: false,
      todos: [],
      defaultMemo: "新規メモ",
    };
  },
  methods: {
    showTodo: function(todo = "", index = "") {
      if (this.isVisible == false) {
        this.isVisible = true;
      } else {
        this.isVisible = false;
      }

      this.index = index;
      if (typeof todo === "object") {
        this.oldTodo = this.defaultMemo;
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

    deleteTodo: function(targetIndex) {
      if (!targetIndex) {
        return;
      }
      this.todos.splice(targetIndex, 1);
      this.isVisible = false;
      this.setTodos();
    },

    setTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>
