<script setup>
import { ref, computed } from 'vue';

const searchText = ref('');
const warningMessage = computed(() =>
  searchText.value.length > 10 ? '10자를 초과했습니다!' : ''
);
</script>

<template>
  <div>
    <!-- v-model : 컴포넌트에서 양방향 바인딩 구현 -->
    <input type="text" v-model="searchText" placeholder="문자 입력" />
    <p>{{ searchText }}</p>
    <p style="color: red">{{ warningMessage }}</p>
  </div>
</template>
