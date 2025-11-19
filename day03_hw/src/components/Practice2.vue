<script setup>
import Practice2Child from './Practice2Child.vue';
import { ref } from 'vue';

const childName = ref('Alice');

const handleGreeting = (message) => {
  console.log(message);
};
</script>

<template>
  <div>
    <Practice2Child :name="childName" @greet="handleGreeting" />
  </div>
</template>
