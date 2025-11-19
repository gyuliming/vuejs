<script>
// 데이터 바인딩과 이벤트 연결하기
export default {
  data() {
    return {
      output: null, //출력칸에 표시되어 사용자에게 보여지는 값
      prev: null, //이전에 입력된 값 또는 연산 결과
      cur: null, //현재 입력된 값
      operator: null, //연산자
      operationActions: {
        //사칙연산을 수행하는 함수를 각각의 객체로 정의
        '+': (n1, n2) => n1 + n2,
        '-': (n1, n2) => n1 - n2,
        '*': (n1, n2) => n1 * n2,
        '/': (n1, n2) => n1 / n2,
      },
    };
  },
  methods: {
    clear() {
      this.output = null;
      this.prev = null;
      this.cur = null;
      this.operator = null;
    },
    calculate(n) {
      // 연산 흐름을 제어하는 함수로 분리한다.
      // 저장된 숫자가 없는데 연산기호를 클릭한 경우 예외처리
      if (!this.cur && !this.prev) {
        alert('숫자를 먼저 입력해야 합니다.');
        return;
      }
      // 사칙연산 기호를 연달아 클릭한 경우 예외처리
      if (this.operator !== '' && !this.cur) {
        alert('연산 기호를 연속해서 누를 수 없습니다.');
        return;
      }
      // 등호를 클릭하여 결과를 노출한 뒤, 다시 등호를 클릭한 경우 처리하지 않음 예외처리
      if (n === '=' && this.prev === this.cur) {
        return;
      }
      this.cur = Number(this.cur);
      if (this.operator !== null) {
        // 사칙연산 기호면 연산 수행
        // 위에서 operatorActions를 객체로 정의했고, 객체의 각 속성은 함수형 값을 가지는 메서드이기 때문에 아래처럼 코드 작성 가능
        this.prev = this.operationActions[this.operator](this.prev, this.cur);
        if (n === '=') {
          this.output = this.prev;
          this.operator = null;
          this.cur = this.prev;
        } else {
          this.output = null;
          this.operator = n;
          this.cur = null;
        }
      } else {
        this.operator = n;
        this.output = null;
        this.prev = this.cur;
        this.cur = null;
      }
    },
    userInput(number) {
      // 사용자가 입력한 숫자 저장
      this.cur = this.cur === null ? number : (this.cur += number);
      this.output = this.cur;
    },
    operation(event) {
      const n = event.currentTarget.value;
      if (n === 'C') {
        this.clear();
      } else if (['+', '-', '*', '/', '='].includes(n)) {
        this.calculate(n);
      } else {
        this.userInput(n); // 사용자가 입력한 숫자 저장 함수 호출
      }
    },
  },
};
</script>
<template>
  <div class="calculator">
    <form name="forms">
      <input v-model="output" type="text" name="output" readonly />
      <input type="button" class="clear" value="C" @click="operation" />
      <input type="button" class="operator" value="/" @click="operation" />
      <input type="button" value="1" @click="operation" />
      <input type="button" value="2" @click="operation" />
      <input type="button" value="3" @click="operation" />
      <input type="button" class="operator" value="*" @click="operation" />
      <input type="button" value="4" @click="operation" />
      <input type="button" value="5" @click="operation" />
      <input type="button" value="6" @click="operation" />
      <input type="button" class="operator" value="+" @click="operation" />
      <input type="button" value="7" @click="operation" />
      <input type="button" value="8" @click="operation" />
      <input type="button" value="9" @click="operation" />
      <input type="button" class="operator" value="-" @click="operation" />
      <input type="button" class="dot" value="." @click="operation" />
      <input type="button" value="0" @click="operation" />
      <input
        type="button"
        class="operator result"
        value="="
        @click="operation"
      />
    </form>
  </div>
</template>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #ffffff;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.calculator {
  width: 287px;
  border: 1px solid #333;
  background-color: #ccc;
  padding: 5px;
}

.calculator form {
  display: grid;
  grid-template-columns: repeat(4, 65px);
  grid-auto-rows: 65px;
  grid-gap: 5px;
}

.calculator form input {
  border: 2px solid #333;
  cursor: pointer;
  font-size: 19px;
}

.calculator form input:hover {
  box-shadow: 1px 1px 2px #333;
}

.calculator form .clear {
  background-color: #ed4848;
}

.calculator form .operator {
  background-color: orange;
}

.calculator form .dot {
  background-color: green;
}

.calculator form input[type='text'] {
  grid-column: span 4;
  text-align: right;
  padding: 0 10px;
}

.calculator form .clear {
  grid-column: span 3;
}

.calculator form .result {
  grid-column: span 2;
}
</style>
