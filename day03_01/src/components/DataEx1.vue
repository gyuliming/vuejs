<script setup>
import { ref } from 'vue';

const count = ref(0); // 기본 자료형
const state = ref({ count: 0 }); // 참조 자료형

console.log(count.value);
console.log(state.value.count);

setTimeout(() => {
  count.value++;
}, 1000); // 콜백함수

setTimeout(() => {
  state.count++;
}, 1000);
</script>

<template>
  <h1>count : {{ count }}</h1>
  <h1>state : {{ state.count }}</h1>
</template>
