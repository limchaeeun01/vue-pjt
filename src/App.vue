<template>
  <div class="name">{{ msg }}</div>
  <div class="name">{{greeting()}}</div>
  <div class="name">{{hello("chaeni")}}</div>
</template>

<script>
  export default{
    setup(){
      const msg = "즐거운 점심시간";

      const greeting = () => {
        return "Hi~~" ;
      }

      const hello = (name) => {
        return `Hi, ${name}`;
      }

      return{
        msg,
        greeting,
        hello
      }
    }
  }
</script>

<style>
  .name{
    color : red;
  }
</style>


