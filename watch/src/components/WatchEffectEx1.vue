<script setup>
import { reactive, ref, watchEffect } from 'vue';
//1.   객체 자료형 속성 count 에 값 0을 할당하여 reactive() 반응형데이터로 만들어 주세요
const count = ref(0);
const state = reactive({ count: 0 });
// 반응형 데이터를 콜백 함수 형태로 사용한 인자로 watch()에게 넘겨주기
// watchEffect는 반응형 데이터를 자동으로 추적 -> 무엇을 watch할지 직접 지정 안해도 됨
// 초기 실행 시 count.value 와 state.count를 읽음 -> 둘 중 하나라도 바뀌면 자동으로 재실행
// watch와 다르게 preValue 제공 X, 의존성 자동 추적 방식
watchEffect(() => {
  console.log(count.value);
  console.log(state.count);
});
</script>

<template>
  <h1>ref : {{ count }}</h1>
  <button @click="count++">ref 증가</button>

  <br />
  <h1>reactive: {{ state.count }}</h1>
  <button @click="state.count++">ref 증가</button>
</template>
