<template>
  <main>
    <div>
      <h4>The current count is...</h4>
      <h1>{{ count }}</h1>
      <button @click="subtractCount">-</button>
      <button @click="addToCount">+</button>
    </div>  
  </main>
</template>

<!-- <script setup>  Composition API
  import { ref } from "vue";
  const count = ref(0);

  const addToCount = () => {
    count.value++;

  }

  const subtractCount = () => {
    if(count.value > 0) {
      count.value--; 
    }
  }
</script> -->

<script> // options API
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    addToCount() {
      this.count++;
    },

    subtractCount() {
      if(this.count > 0) {
        this.count--;
      }
    }
  }

}
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