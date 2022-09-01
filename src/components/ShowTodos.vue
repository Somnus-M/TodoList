<template>
    <ul class="todo-main">
        <ShowOneThing/>
    </ul>
</template>

<script>
    import ShowOneThing from './ShowOneThing.vue'
    
    export default {
        name:'ShowTodos',
        components:{ShowOneThing}
    }
</script>

<style>

</style>