<template>
  <transition 
    name="animate__animated animate__bounce"
    appear
    enter-active-class="animate__fadeInDown"
    leave-active-class="animate__fadeOutDown"
  >
    <li>
      <label>
        <input
          type="checkbox"
          :checked="todos.isFinish"
          @change="handleChecked(todos.id)"
        />
        <span v-show="!todos.isEdit">{{ todos.title }}</span>
        <input
          type="text"
          :value="todos.title"
          v-show="todos.isEdit"
          @blur="finishEdit(todos,$event)"
          ref="inputTitle"
        />
      </label>
      <button class="btn btn-danger" @click="handleTodo(todos.id)">删除</button>
      <button class="btn btn-edit" @click="handleEdit(todos)" v-show="!todos.isEdit">编辑</button>
    </li>
  </transition>
</template>

<script>
import 'animate.css'
export default {
  name: "ShowOneThing",
  props: ["todos"],
  methods: {
    handleChecked(id) {
      this.$bus.$emit("checkTodo", id)
    },
    handleTodo(id) {
      if (confirm("确定要删除吗？")) {
        this.$bus.$emit("deleteTodo", id)
      }
    },
    handleEdit(todos) {
      if (todos.hasOwnProperty('isEdit')) {
        todos.isEdit = true
      } else {
        console.log('@')
        this.$set(todos, 'isEdit', true)
      }
      this.$nextTick(()=>{
        this.$refs.inputTitle.focus()
      })
    },
    finishEdit(todos,e) {
      todos.isEdit = false
      this.$bus.$emit('updateTitle',todos.id,e.target.value)
    },
  },
};
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
li:hover {
  background-color: #ddd;
}
li:hover button {
  display: block;
}
</style>