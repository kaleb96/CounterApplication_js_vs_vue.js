<template>
  <div>
    <header>
      <h1>Calculator</h1>
    </header>
    <main>
      <div>
          
          <div class="buttonForm">
            <div>첫번째 숫자{{ firstNum }}</div>
            <div>두 번째 연산자 {{ operatorStr }}</div>
            <div>세 번째 숫자 {{ secondNum }}</div>
            <div>네 번째 결과 지 {{ firstNum }} {{ operatorStr }} {{ secondNum }} = </div>
            <div>결과 flag {{ flag }}</div>
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


const firstNum = ref(0);
const operatorStr = ref('');
const secondNum = ref(0);
const flag = ref('');

const matrix = ref([
  ['c', '<'],
  ['7', '8', '9', '/'],
  ['4', '5', '6', 'x'],
  ['1', '2', '3', '-'],
  ['.', '0','=','+']
])


const inputNum = (param) => { //버튼 input값에 따른 연산 판단
  
  let regex = /[0-9.]/g;

 
  if(regex.test(param)) { // 정수 또는 '.' 인 경우
    
    if(operatorStr.value == '') { // firstNum
      
      if(firstNum.value == 0) {
        firstNum.value = param;
      } else {
        firstNum.value += param;
      }

    } else {  // secondeNum
      
      if(secondNum.value == 0) {
        secondNum.value = param;
      } else {
        secondNum.value += param;
      }
    }
  
  } else { // 연산자인 경우
    
    if((param == '=')) { // = 인경우, firstNum, operatorStr, secondNum이 있는 경우 -> 결과 연산!
      
      if(operatorStr != '') {

        computeResult(operatorStr);
      }

    } else { // 연산자인 경우

      operatorStr.value = param;
    }
  }

}

const computeResult = (param) => { // 연산자 구분, 계산
  
  let co = param.value; 
  let value1 = parseFloat(firstNum.value);
  let value2 = parseFloat(secondNum.value);
  let result = '';
  switch (co) {

    case '-':
      result = value1 - value2;
      formatData(result);
      break;
    
    case '+':
      result = value1 + value2;
      formatData(result);
      break;
    
    case '/':
      result = value1 / value2;
      formatData(result);
      break;
    
    case '%':
      result = value1 % value2;
      formatData(result);
      break;
    
    case 'x':
    result = value1 * value2;
    formatData(result);
    break;  

    default:
      console.log('정의 되지 않은 계산입니다.');
      formatData(result);
      break;
  }
}

const formatData= (param) => { // 데이터 초기화
    
    firstNum.value = param;
    secondNum.value = 0;
    operatorStr.value = '';
    flag.value = param;
}

</script>

<style>
</style>