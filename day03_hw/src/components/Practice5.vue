<script setup>
import { ref } from 'vue';
const inputValue = ref('');
const inputRef = ref(null);

const click = () => {
  inputRef.value.focus();
  alert(inputValue.value);
};
</script>

<template>
  <input type="text" v-model="inputValue" ref="inputRef" />
  <button @click="click">버튼</button>
</template>
