<template>
  <div class="todo">
    <form @submit.prevent>
      <textarea type="text" v-model="todo" />
      <input type="hidden" v-model="oldTodo" />
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
      oldTodo: "",
      index: "",
    };
  },
  props: {
    value: Object,
  },
  mounted() {
    this.todo = this.value.oldTodo;
    this.oldTodo = this.value.oldTodo;
    this.index = this.value.index;
  },
  methods: {
    saveTodo() {
      if (this.oldTodo != "") {
        this.$emit("delTodo", this.index);
      }
      this.$emit("addTodo", this.todo);
      this.todo = "";
    },
    deleteTodo: function() {
      this.$emit("delTodo", this.index);
      this.todo = "";
    },
  },
};
</script>
