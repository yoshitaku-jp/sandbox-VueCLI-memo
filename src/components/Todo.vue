<template>
  <div class="todo">
    <form v-on:submit.prevent>
      <textarea type="text" v-model="todo" />
      <input type="hidden" v-model="oldTodo" />
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
      oldTodo: "",
    };
  },
  props: ["value"],
  mounted() {
    this.todo = this.value.oldTodo;
    this.oldTodo = this.value.oldTodo;
  },
  methods: {
    saveTodo: function() {
      if (this.oldTodo != "") {
        this.$emit("delTodo", this.oldTodo);
      }
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
