<template>
  <div class="container">
    <h2>To-Do List Page</h2>

    <TodoSearch @search-todo="filteredTodos"/>


    <TodoSimpleForm @add-todo="addTodo"/>

    <div v-if="todos.length==0" style="color : red;">
        추가된 일정이 없습니다.
    </div>

    <TodoList :todos="filterTodos"
            @toggle-todo="toggleTodo"
            @delete-todo="onDelete"/>


  </div>
</template>

<script>
import {ref, computed} from 'vue';
import TodoSimpleForm from './components/TodoSimpleForm.vue';
import TodoList from './components/TodoList.vue';
import TodoSearch from './components/TodoSearch.vue';
export default {
    components : {
        TodoSimpleForm,
        TodoList,
        TodoSearch
    },
    setup(){
        const todos = ref([]);
        const search = ref('');

        const filteredTodos = (searchTxt) => {
            search.value = searchTxt.value;
            console.log("debug >>> filteredTodos searchTxt, ", search.value);
        };

        const filterTodos = computed(() => {
            if(search.value){
                return todos.value.filter( todo => {
                    return todo.subject.includes(search.value);
                })
            }
            return todos.value;
        });

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
            filterTodos,
            addTodo,
            onDelete,
            toggleTodo,
            filteredTodos
        }
    }

}
</script>

<style>

</style>