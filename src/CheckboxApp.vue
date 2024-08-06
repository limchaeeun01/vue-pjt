<template>
  <div class="container">
    <h2>List</h2>
    <form @submit.prevent="onSubmit" class="d-flex">
        <div class="flex-grow-1 mr-2">
            <input class="form-control"
                    type="text"
                    placeholder="Add Your To-Do"
                    v-model="todo">
        </div>
        <div>
            <button class="btn btn-primary" 
                    type="submit"
                    @click="updateData">Add</button>
        </div>

    </form>

    

    <div v-show="notData" style="color : red;">
        추가된 일정이 없습니다.
    </div>

    <div v-for="(data, index) in todos" 
            :key="data.id"
            class="card mt-2">
        <div class="card-body p-2 d-flex align-items-center">
            <div class="form-check flex-grow-1">
                <input type="checkbox" 
                    class="form-check-input"
                    v-model="data.completed">
                <label class="form-check-label"
                    :style="data.completed ? todoStyle : {}">
                    {{ data.subject }}
                </label>
            </div>
            <div>
                <button class="btn btn-danger btn-sm"
                        type="submit"
                        @click="deleteData(index)">Delete</button>
            </div>
        </div>
    </div>


  </div>
</template>

<script>
import {ref} from 'vue';
export default {
    setup(){
        let hasError = ref(false);
        let notData = ref(false);

        const todo = ref('');
        const todos = ref([]);

        if(todos.value.length == 0){
            notData.value = true
        }else{
            notData.value = false;
        }

        //클래스 바인딩
        const todoStyle = {
            textDecoration : 'line-through',
            color : 'gray'
        }

        const onSubmit = () =>{
            if(todo.value != ''){
                todos.value.push({
                    id: todos.value.length + 1,
                    subject: todo.value,
                    completed : false
                });
                todo.value = ''; 
                hasError.value = false;
                notData.value = false;
            }else{
                hasError.value = true;
            }
        };

        const deleteData = (index) => {
            todos.value.splice(index, 1);
            if(todos.value.length == 0){
                notData.value = true;
            }
        };


        return{
            todo,
            todos,
            notData,
            hasError,
            deleteData,
            todoStyle
        }
    }

}
</script>

<style>
    .todo{
        color : gray;
        text-decoration: line-through;
    }
</style>