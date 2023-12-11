<template>
  <div> 
    <header>
      <h1>Calculator</h1>
    </header>
      <div>
        <v-container class="text-center">
         <v-row justify="center">
            <v-col md="3">
            <v-btn min-width="255" max-width="255" >
            <span v-if="!secondNum">{{ firstNum }}</span>
            <span v-if="!secondNum">{{ operatorStr }}</span>
            <span v-if="secondNum">{{ firstNum }}{{ operatorStr }}{{ secondNum }} = </span></v-btn> <br>
            <span v-for="(row, idx) in matrix" :key="idx"> <v-btn @click="inputNum(row[cIdx])" v-for="(cell, cIdx) in row" :key="cIdx">{{ row[cIdx] }}</v-btn>
            </span>
          </v-col>
        </v-row>
       </v-container>
      </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const firstNum = ref(0);
const operatorStr = ref('');
const secondNum = ref(0);
const flag = ref('');
const seq = ref(1);
const matrix = ref([
  ['', '', 'c', '\u{21A4}'],
  ['7', '8', '9', '/'],
  ['4', '5', '6', 'x'],
  ['1', '2', '3', '-'],
  ['.', '0','=','+']
])


// 버튼 입력시 데이터 처리
const inputNum = (param) => {
  
  let regex = /[0-9.]/g;
  let seqNum =  seq.value;
  let test = regex.test(param);

  if(test) { // firstNum 또는 secondNum인 경우

      if(seqNum === 1){ // firstNum
        
        if(operatorStr.value == '') { // 연산자 입력시 secondNum으로

          if(firstNum.value == 0) {
            firstNum.value = param;
          
          } else {
            firstNum.value += param;
          }

        } else {
          return seq.value = 2
        }
      }
      
      if(seqNum === 2) { // secondNum
        
        if(secondNum.value == 0) {
          secondNum.value = param;
        } else {
          secondNum.value += param;
        }
      }

      if(seqNum === 3) {
        
        seq.value = 1;
        firstNum.value = 0;
        secondNum.value = 0;
        operatorStr.value = '';
        flag.value = '';
      }
    
    } else  { // operators
      seq.value = 2;
    if((param === '=')) { // 결과 연산

      if(param != '') { // 결과연산일때 모든 값이 있을 경우
        computeResult(operatorStr);
      }
    
    } else { // Clear all, Clear Entry 인 경우
      
      if(param == 'c') { // c버튼 Clear All
        
        seq.value = 1;
        firstNum.value = 0;
        secondNum.value = 0;
        operatorStr.value = '';
        flag.value = '';

      } else if(param == '\u{21A4}') { // < 버튼 Clear Entry

        if(flag.value == '') { // 첫번째 결과 연산인 경우

          let value1 = firstNum.value;
          let value2 = secondNum.value;
          let value3 = operatorStr.value;

          if(value2 == 0 && value3 == '') 
            seq.value=1;
          console.log('values' + value1 + '  v2= ' + value2+ ' v3 = ' +value3);
          clearEntry(value1, value2, value3);
        
        } else { // 2번째 결과 연산 인경우

          seq.value = 1;
          firstNum.value = 0;
          secondNum.value = 0;
          operatorStr.value = '';
        }
        
      }else {
        
        operatorStr.value = param;
      }
    }
  }
}

 // 연산자 구분, 계산
const computeResult = (param) => {
  
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

// 연산 이후 데이터 초기화
const formatData= (param) => { 
    
    seq.value = 3; //seq를 3으로 줄 경우 숫자를 입력하면 바로 clear all
    firstNum.value = param;
    secondNum.value = 0;
    operatorStr.value = '';
    flag.value = param;
}

// Clear Entry 취소 
const clearEntry = (value1, value2, value3) => { 
  let nv = '';
  
  console.log('seq.value = ' + seq.value)
  
  if(seq.value == 1 && value3 == '') { // firstNum에서 ClearEntry 작동
    console.log('firstNum ClearEntry 작동');
    
    if(firstNum.value != 0) {
      nv = [...value1].splice(0, value1.length-1);
      firstNum.value = nv.join('');
    } else {
      firstNum.value = 0;
    }
  } 
  
  if(seq.value == 2 && value2 != 0) { // secondNum에서 ClearEntry 작동
    
    console.log('secondNum ClearEntry 작동');
    nv = [...value2].splice(0, value2.length-1);  
    secondNum.value = nv.join('');
  }  
  
  if(value1 != 0 && value3 != ''){
    console.log('작동 X');
      // firatNum, Operators있는 경우 Clear Entry 작동 X
  }

}
</script>

<style>

.col {
  max-width: 300px;
  min-width: 300px;
}

.result {
  text-align:left;
}
</style>