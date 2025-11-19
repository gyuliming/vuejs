<script setup>
import { computed, ref } from 'vue';

const number = ref(5);
const doubleNumber = computed(() => number.value * 2);

// 지정한 값을 부모 컴포넌트에서 접근가능하게 emit
defineExpose({
  number,
  doubleNumber,
});
</script>

<template>
  <h1>{{ number }}</h1>
  <h1>{{ doubleNumber }}</h1>
</template>
