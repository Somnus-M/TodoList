<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <AddTodoList :add="add"/>
        <ShowTodos :todos="todos"/>
        <FinishTodo/>
      </div>
    </div>
  </div>
</template>

<script>
//引入添加项目
  import AddTodoList from './components/AddTodoList.vue'
//引入完成项目
  import FinishTodo from './components/FinishTodo.vue'
//引入展示项目
  import ShowTodos from './components/ShowTodos.vue'

  export default {
    name: 'App',
    components: {
      AddTodoList,
      FinishTodo,
      ShowTodos
    },
    data() {
          return {
            todos:[
              {
                id:'001',
                title:'抽烟',
                isFinish:true
              },
              {
                id:'002',
                title:'喝酒',
                isFinish:false
              },
              {
                id:'003',
                title:'烫头',
                isFinish:true
              },
            ]
          }
        },
    methods: {
      add(oneThing){
        this.todos.unshift(oneThing)
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
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
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
