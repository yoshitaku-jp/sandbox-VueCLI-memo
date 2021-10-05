<template>
  <div class="todo">
    <form v-on:submit.prevent>
      <input type="text" v-model="newItem" />
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
      newItem: "",
    };
  },
  methods: {
    saveTodo: function() {
      this.$emit("addTodo", this.newItem);
      this.newTodo = "";
    },
  },
};
</script>
