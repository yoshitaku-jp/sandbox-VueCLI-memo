<template>
  <div class="todo">
    <form @submit.prevent>
      <textarea type="text" v-model="todo" />
      <button @click="saveTodo">編集</button>
      <button @click="deleteTodo">削除</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      todo: "",
      index: "",
    };
  },
  props: {
    targetTodo: String,
    targetIndex: Number,
  },
  mounted() {
    this.todo = this.targetTodo;
    this.index = this.targetIndex;
  },
  methods: {
    saveTodo() {
      this.$emit("addTodo", this.todo, this.index);
      this.todo = "";
    },
    deleteTodo: function() {
      this.$emit("delTodo", this.index);
      this.todo = "";
    },
  },
};
</script>
