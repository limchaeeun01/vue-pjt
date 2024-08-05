<template>
  <div v-if="toggle">true</div>
  <div v-else>false</div>
  <button @click="onToggle">Toggle</button>
</template>

<script>
import {ref} from 'vue';
export default {
    setup(){
        const toggle = ref(false);
        const onToggle = () => {
            toggle.value = !toggle.value;
        }

        return{
            toggle,
            onToggle
        }
    }
}
</script>

<style>

</style>