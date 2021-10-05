<template>
  <div class="todolist">
    <h1>Todoアプリ</h1>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <span>{{ todo.item }}</span>
      </li>
    </ul>
    <button v-on:click="showTodo">＋</button>
    <div v-if="toggle"><Todo @addTodo="saveTodo" /></div>
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
      todos: [
        {
          index: 1,
          item: "todo1",
        },
        {
          index: 2,
          item: "todo2",
        },
      ],
    };
  },
  methods: {
    showTodo: function() {
      this.toggle == true ? (this.toggle = false) : (this.toggle = true);
    },
    saveTodo: function(newItem) {
      const newTodo = newItem;
      if (!newTodo) {
        return;
      }
      console.log(newTodo);
      const obj = {
        index: this.todos.length + 1,
        item: newTodo,
      };
      this.todos.push(obj);
      console.log(this.todos);
    },
  },
};
</script>
