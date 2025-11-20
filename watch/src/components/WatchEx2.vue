<script setup>
import { ref, watch } from 'vue';
//1.   객체 자료형 속성 count 에 값 0을 할당하여 반응형데이터로 만들어 주세요
// ref로 객체를 감싸면 기본적으로 내부 속성 변화를 감지하지 못함 -> deep: true 필요(내부 속성 추적)
// state.count++는 내부 속성 변화지만 watch(state)는 ref 자체가 완전히 새로운 객체로 바뀌어야 실행되기 때문.
const state = ref({ count: 0 });

watch(
  state,
  (currentValue, preValue) => {
    console.log(currentValue, preValue);
  },
  { deep: true }
);
</script>

<template>
  <h1>ref : {{ state.count }}</h1>
  <button @click="state.count++">ref 증가</button>
</template>
