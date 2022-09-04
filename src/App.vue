<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <AddTodoList @add="add" />
        <ShowTodos
          :todos="todos"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        />
        <FinishTodo 
          :todos="todos" 
          @checkedTodos="checkedTodos"
          @clearDoneTodos="clearDoneTodos"
        />
      </div>
    </div>
  </div>
</template>

<script>
//引入添加项目
import AddTodoList from "./components/AddTodoList.vue";
//引入完成项目
import FinishTodo from "./components/FinishTodo.vue";
//引入展示项目
import ShowTodos from "./components/ShowTodos.vue";

export default {
  name: "App",
  components: {
    AddTodoList,
    FinishTodo,
    ShowTodos,
  },
  data() {
    return {
      todos:JSON.parse(localStorage.getItem('todos')) || [],
    }
  },
  methods: {
    //从AddtodoList添加事情
    add(oneThing) {
      this.todos.unshift(oneThing)
    },
    //勾选或者不勾选
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          todo.isFinish = !todo.isFinish;
        }
      })
    },
    //删除事件
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => {
          return todo.id !== id
      })
    },
    //全选或者不选
    checkedTodos(done){
      this.todos.forEach(todo=>todo.isFinish = done)
    },
    //清除已完成的任务
    clearDoneTodos(){
      this.todos=this.todos.filter((todo)=> !todo.isFinish)
    }
  },
  watch: {
    todos:{
      deep:true,
      handler(value){
        localStorage.setItem('todos',JSON.stringify(value))
      }
    }
  },
}
</script>

<style>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
