<template>

    <div v-for="(data, index) in todos" 
            :key="data.id"
            class="card mt-2">
        <div class="card-body p-2 d-flex align-items-center">
            <div class="form-check flex-grow-1">
                <input type="checkbox" 
                    class="form-check-input"
                    :value="data.completed"
                    @change="toggleTodo(index)">
                <label class="form-check-label"
                    :style="data.completed ? todoStyle : {}">
                    {{ data.subject }}
                </label>
            </div>
            <div>
                <button class="btn btn-danger btn-sm"
                    type="submit"
                    @click="onDelete(index)">Delete</button>
            </div>
        </div>
    </div>
</template>

<script>
/*
props 사용시 주의점
-props 전달된 데이터는 One-Way Data Flow(부모(TodoApp)가 자식(TodoList)에게 보내는 데이터)
-그래서 자식에서 데이터 변경 X
*/
export default {
    props : {
        todos : {
            type : Array,
            required : true
        }
    },
    setup(props, context){
        const todoStyle = {
            textDecoration : 'line-through',
            color : 'gray'
        }

        const toggleTodo = (index) => {
            context.emit('toggle-todo', index);
        }

        return{
            todoStyle,
            toggleTodo
        }
    }

}
</script>

<style>

</style>