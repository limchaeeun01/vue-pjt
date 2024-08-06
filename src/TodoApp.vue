<template>
  <div class="container">
    <h2>To-Do List Page</h2>
    <TodoSimpleForm @add-todo="addTodo"/>

    <div v-if="todos.length==0" style="color : red;">
        추가된 일정이 없습니다.
    </div>

    <TodoList :todos="todos"
            @toggle-todo="toggleTodo"/>


  </div>
</template>

<script>
import {ref} from 'vue';
import TodoSimpleForm from './components/TodoSimpleForm.vue';
import TodoList from './components/TodoList.vue';
export default {
    components : {
        TodoSimpleForm,
        TodoList
    },
    setup(){
        const todos = ref([]);

        const todoStyle = {
            textDecoration : 'line-through',
            color : 'gray'
        }


        const addTodo = (data) => {
            console.log("debug >>> form emit data addTodo, ", data);
            todos.value.push(data);
        }

        const onDelete = (index) => {
            console.log("debug >>>> delete btn click index = " , index); 
            todos.value.splice(index,1);
        } 

        const toggleTodo = (index) => {
            console.log("debug >>> toggleTodo index, ", index);
            console.log("debug >>> toggleTodo before, ", todos.value[index]);
            todos.value[index].completed = !todos.value[index].completed;
            console.log("debug >>> toggleTodo after, ", todos.value[index]);
        }
        return{
            todos,
            todoStyle,
            addTodo,
            onDelete,
            toggleTodo
        }
    }

}
</script>

<style>

</style>