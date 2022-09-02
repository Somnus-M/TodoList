<template>
  <div class="todo-footer" v-show="allTotal">
    <label>
      <!-- <input type="checkbox"  :checked="checkedAll" @change="handleChecked"/> -->
      <input type="checkbox" v-model="checkedAll" />
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ allTotal }}
    </span>
    <button class="btn btn-danger" @click="handleClear">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "FinishTodo",
  props: ["todos", "checkedTodos", "clearDoneTodos"],
  computed: {
    doneTotal() {
      return this.todos.reduce((pre, todo) => pre + (todo.isFinish ? 1 : 0), 0);
    },
    allTotal() {
      return this.todos.length;
    },
    checkedAll: {
      get() {
        return this.doneTotal === this.allTotal && this.allTotal > 0;
      },
      set(value) {
        this.checkedTodos(value);
      },
    },
  },
  methods: {
    handleChecked(e) {
      this.checkedTodos(e.target.checked);
    },
    handleClear() {
      this.clearDoneTodos();
    },
  },
};
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>