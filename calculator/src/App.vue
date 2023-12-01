<template>
  <div>
    <header>
      <h1>Calculator</h1>
    </header>
    <main>
      <div class="matrix">
          <div v-for="(num, idx) in matrix" :key="idx">
              <button>{{ 9 - idx }}</button> 
          </div>
      </div>
    </main>    
  </div>
</template>

<script setup>

import { ref} from 'vue'

const matrix = ref(9);

</script>

<style>

main {
  background-color: aliceblue;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.matrix {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}

.col {
  flex:1;
  text-align: center;
  padding:10px;
}
</style>