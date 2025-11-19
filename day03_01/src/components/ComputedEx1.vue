<script setup>
import { computed, reactive, ref } from 'vue';

const refCount = ref(0);
const reactiveCount = reactive({ count: 0 });

// ref() 데이터를 활용할 때는 항상 .value 속성 필요 O
const refDoubleCount = computed(() => refCount.value * 2);
// reactive() 데이터를 활용할 때는 .value 속성 필요 X
const reactiveDoubleCount = computed(() => reactiveCount * 2);

// computed로 계산된 데이터를 출력할 때는 둘다 .value 속성 사용
console.log(refDoubleCount.value);
console.log(reactiveDoubleCount.value);
</script>

<template>
  <h1>{{ refDoubleCount }}</h1>
  <h1>{{ reactiveDoubleCount }}</h1>
</template>
