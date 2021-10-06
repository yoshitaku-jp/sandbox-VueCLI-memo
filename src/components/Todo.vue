<template>
  <div class="todo">
    <form v-on:submit.prevent>
      <input type="text" v-model="todo" />
      <button v-on:click="saveTodo">編集</button>
      <button v-on:click="deleteTodo">削除</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data: function() {
    return {
      todo: "",
    };
  },
  methods: {
    saveTodo: function() {
      this.$emit("addTodo", this.todo);
      this.todo = "";
    },
    deleteTodo: function() {
      this.$emit("delTodo", this.todo);
      this.todo = "";
    },
  },
};
</script>
