<template>
  <div class="todo">
    <form v-on:submit.prevent>
      <input type="text" v-model="newItem" />
      <button v-on:click="addTodo">編集</button>
      <button v-on:click="addTodo">削除</button>
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
};
</script>
