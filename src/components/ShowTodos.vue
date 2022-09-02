<template>
    <ul class="todo-main">
        <ShowOneThing 
          v-for="todo in todos" 
          :key="todo.id" 
          :todos="todo"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        />
    </ul>
</template>

<script>
    import ShowOneThing from './ShowOneThing.vue'
    
    export default {
        name:'ShowTodos',
        components:{ShowOneThing},
        props:['todos','checkTodo','deleteTodo']
    }
</script>

<style scoped>
  /*main*/
  .todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
  }

  .todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
  }
</style>