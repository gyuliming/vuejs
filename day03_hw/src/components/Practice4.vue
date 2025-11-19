<script setup>
import { reactive, computed } from 'vue';
const cart = reactive({
  item1: {
    price: 1000,
    count: 2,
  },
  item2: {
    price: 2000,
    count: 3,
  },
});

const totalPrice = computed(
  () =>
    cart.item1.price * cart.item1.count + cart.item2.price * cart.item2.count
);
</script>

<template>
  <div>
    <p>상품1 : {{ cart.item1.price }}원 x {{ cart.item1.count }}</p>
    <p>상품2 : {{ cart.item2.price }}원 x {{ cart.item2.count }}</p>
    <p>총합 : {{ totalPrice }}원</p>
  </div>
</template>
