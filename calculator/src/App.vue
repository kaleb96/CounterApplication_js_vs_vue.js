<template>
  <div>
    <header>
      <h1>Calculator</h1>
    </header>
    <main>
      <div>
          
          <div class="buttonForm">
            <!-- <div>Count Num</div>
            <button>c</button>
            <button>&#9003;</button> <br>
            <button>7</button>
            <button>8</button>
            <button>9</button> 
            <button>&divide;</button> <br>
            <button>4</button>
            <button>5</button>
            <button>6</button> 
            <button>x</button> <br>
            <button>1</button>
            <button>2</button>
            <button>3</button> 
            <button>-</button> <br>
            <button>.</button>
            <button>0</button>
            <button>=</button>
            <button>+</button> -->
            <div>{{ count }}</div>
            <span v-for="(row, idx) in matrix" :key="idx"> <br>
            <button  @click="inputNum(row[cIdx])" v-for="(cell, cIdx) in row" :key="cIdx"> {{ row[cIdx] }} </button>
            </span>
          </div>
      </div>
    </main>    
  </div>
</template>

<script setup>
import { ref } from 'vue'

const count = ref('');

const matrix = ref([
  ['c', '<'],
  ['7', '8', '9', '/'],
  ['4', '5', '6', 'x'],
  ['1', '2', '3', '-'],
  ['.', '0','=','+']
])

const inputNum = (num) => {
  // console.log('inputNum = ' + num );
  count.value = num;
}

</script>

<style>

</style>