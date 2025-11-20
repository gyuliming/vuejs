<script setup>
// 자식컴포넌트(현재)에서는 부모컴포넌트(App.vue)에서 전달한 이벤트를 defineEmits() 받는다.
import { defineEmits } from 'vue';
// 부모 이벤트를 받을 수 있도록 defineEmits 사용 / 부모의 count 증가, 부모의 state-count 증가
const emit = defineEmits(['count-increment', 'state-count-increment']);

// increment 함수는 부모에게 count-increment 이벤트를 보냄
const increment = () => {
  emit('count-increment');
};
</script>

<template>
  <!-- 버튼 클릭하면 자식 → 부모로 "count-increment" 이벤트 전달 -->
  <button @click="increment">count증가</button>

  <!-- increment() 함수 없이 직접 emit 호출해서 "state-count-increment" 이벤트를 부모에게 보냄 -->
  <button @click="emit('state-count-increment')">state.count 증가</button>
</template>
