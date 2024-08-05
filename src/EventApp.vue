<template>
    <div>
        {{ name }}
    </div>
    <input type="text" v-model="name">
    <div class="container">
        <button class="btn btn-primary"
            @click="updateData">Click</button>
    </div>
</template>

<script>

import {ref} from 'vue';

export default {
    setup(){
        let name = ref('chaeni');
        let type = ref('number');
        const updateData = () =>{
            //name.value = "dynamic data";
            //type.value = "text";
            console.log(name.value);
        };

        return{
            updateData,
            name,
            type,
        }
    }
}
</script>

<style>

</style>