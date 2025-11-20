<script setup>
import { ref, watch, watchEffect, watchPostEffect } from 'vue';
const message = ref('');
const messageP = ref(null);

// DOM : HTML을 JavaScript로 조작 가능하게 만든 구조가 바로 DOM
// InnerText : DOM 요소 안에 있는 텍스트(글자 내용) 을 가져오거나 바꾸는 속성

// watch : message 값이 바뀌면 실행
// DOM 업데이트 전 or 중에 실행, ref DOM이 최신아 아닐수도 있음
watch(message, () => {
  if (message.value) {
    console.log(`watch: ${messageP.value.innerText} `);
  }
});

// watchEffect : 자동 추적, messageP.innerText가 DOM 업데이트 후에 읽힘
watchEffect(
  () => {
    if (message.value) {
      console.log(`watchEffect: ${messageP.value.innerText} `);
    }
  },
  { flush: 'post' }
);

// watchPostEffect : Vue가 DOM을 바꾸고 난 뒤 실행, watchEffect와 동일하게 업데이트 이후 안전하게 DOM 접근 가능
watchPostEffect(() => {
  if (message.value) {
    console.log(`watchPostEffect: ${messageP.value.innerText} `);
  }
});
</script>

<template>
  <div>
    <input v-model="message" placeholder="메시지를 입력하세요" />
    <p ref="messageP">{{ message }}</p>
  </div>
</template>
