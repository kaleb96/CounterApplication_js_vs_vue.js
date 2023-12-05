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
            <div>{{ addStr }}</div>
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

// const count = ref('');
// const operators = ref('');
const addStr = ref('');

const matrix = ref([
  ['c', '<'],
  ['7', '8', '9', '/'],
  ['4', '5', '6', 'x'],
  ['1', '2', '3', '-'],
  ['.', '0','=','+']
])

const inputNum = (param) => {
  // console.log('inputNum = ' + num );
  let value = ''
  if(isNaN(param)) { //파라미터가 정수인 경우
    
    value = param;
    // console.log('count.value = ' + count.value);

  } else { // 기호인 경우
    // operators.value = param;
    value = param;
    // console.log('operators.value = ' + operators.value);

  }
  addStr.value += value; //문자열 합치기


}

</script>

<style>
</style>