<template>
  <div>
    <header>
      <h1>Calculator</h1>
    </header>
    <main>
      <div>
          
          <div class="buttonForm">
            <div>{{ addStr }}</div>
            <div></div>
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
  

    if(!(isNaN(param))) { // 정수인 경우
      value = param;
    }
  
    if(isNaN(param)) { // 연산자인 경우
      value = param;
    }
  
  addStr.value += value; //문자열 합치기

  // return addStr하거나 다른 콜백 함수를 통해서 다시 받기
}

</script>

<style>
</style>