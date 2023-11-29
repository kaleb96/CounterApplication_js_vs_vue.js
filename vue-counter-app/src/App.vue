<template>
  <main>
    <div>
      <h4>The current count is...</h4>
      <h1>{{ count }}</h1>
      <button @click="countBtn">-</button>
      <button @click="countBtn">+</button>
    </div>  
  </main>
</template>

<script setup>
  import {ref} from "vue";
  const count = ref(0);

</script>

<style scoped>
  main {
    background-color: aliceblue;
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  div {
    text-align: center;
  }
</style>