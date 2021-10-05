<template>
  <div class="todolist">
    <h1>Todoアプリ</h1>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <span>{{ todo.item }}</span>
      </li>
    </ul>
    <button v-on:click="showTodo">＋</button>
    <div v-if="toggle">aaa</div>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data: function() {
    return {
      newItem: "",
      toggle: true,
      todos: [
        {
          index: 1,
          item: "aaa",
        },
        {
          index: 2,
          item: "bbb",
        },
      ],
    };
  },
  methods: {
    showTodo: function() {
      this.toggle == true ? (this.toggle = false) : (this.toggle = true);
    },
  },
};
</script>
