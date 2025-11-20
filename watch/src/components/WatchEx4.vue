<script setup>
import { reactive, ref, watch } from 'vue';
//1.   객체 자료형 속성 count 에 값 0을 할당하여 reactive() 반응형데이터로 만들어 주세요
const state = reactive({ count: 0 });
// 반응형 데이터를 콜백 함수 형태로 사용한 인자로 watch()에게 넘겨주기
watch(
	() => state.count,
	(currentValue, preValue) => {
		console.log(currentValue, preValue);
	}
);
</script>

<template>
	<h1>ref : {{ state.count }}</h1>
	<button @click="state.count++">ref 증가</button>
</template>
