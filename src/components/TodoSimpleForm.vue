<template>
    <form @submit.prevent="onSubmit" class="d-flex">
        <div class="flex-grow-1 mr-2">
            <input class="form-control"
                    type="text"
                    placeholder="Add Your To-Do"
                    v-model="todo">
        </div>
        <div>
            <button class="btn btn-primary" 
                    type="submit">Add</button>
        </div>

        <div v-show="hasError" style="color : red;">
            This field cannot be empty!!
        </div>

    </form>
  
</template>

<script>
import {ref} from 'vue';
export default {
    setup(props, context){
        const todo = ref('');
        const hasError = ref(false);
        const onSubmit = () => {
            if(todo.value != ''){
                context.emit('add-todo', {
                    id : Date.now(),
                    subject : todo.value,
                    completed : false
                });
                todo.value = ''; 
                hasError.value = false;
            }else{
                hasError.value = true;
            }
        }

        return{
            todo,
            hasError,
            onSubmit
        }

    }
}
</script>

<style>

</style>