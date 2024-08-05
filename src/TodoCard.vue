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

    <div v-show="hasError" style="color : red;">
            This field cannot be empty!!
        </div>

    <div v-for="data in todos" 
            :key="data.id"
            class="card mt-2">
        <div class="card-body p-2">
            {{ data.subject }}
        </div>
    </div>


    {{ todos }}
  </div>
</template>

<script>
import {ref} from 'vue';
export default {
    setup(){
        let hasError = ref(false);
        const todo = ref('');
        const todos = ref([
            {id : 1, subject : '파일럿 영화보기'},
            {id : 2, subject : '충분한 휴식'}
        ]);

        const updateData = () =>{
            if(todo.value != ''){
                todos.value.push({
                    id: todos.value.length + 1,
                    subject: todo.value
                });
                todo.value = ''; 
                hasError.value = false;
            }else{
                hasError.value = true;
            }
        };

        return{
            todo,
            todos,
            hasError,
            updateData
        }
    }

}
</script>

<style>

</style>