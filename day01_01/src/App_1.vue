<script>
export default {
  // 데이터 정의 : 컴포넌ㄴ트 전반에 걸쳐서 사용할 값
  // data: function () {
  //   return {};
  // },
  data() {
    return {
      // name: 'ssg',
      // age: 20,
      // message: '<h1>Hello VueJs!</h1>',
      // message: 'Hello , Vue!!',
      // className: 'red-color',
      // visible: true,
      // unvisible: false,

      // condition: 'A',
      condition: true,

      names: ['ssg1', 'ssg2', 'ssg3'],
      user: [
        { key: 'name', value: 'John' },
        { key: 'age', value: 20 },
        { key: 'gender', value: 'male' },
      ],
    };
  },
  methods: {
    clickHandler(event, message) {
      // alert('버튼이 눌렸다');
      console.log(event);
      console.log(message);
    },
  },
};
</script>
<template>
  <!-- <p>성함 : {{ name }}</p>
  <p>연령 : {{ age }}</p> -->
  <!-- <div v-html="message"></div> -->
  <!-- <div v-text="message"></div> -->
  <!-- <div v-pre="message"></div> -->
  <!-- <div v-pre>{{ message }}</div> -->

  <!-- <h1 v-bind:class="className">안녕하세요</h1> -->
  <!-- <h1 :class="className">안녕하세요</h1> -->
  <!-- 
  <p v-if="visible">보임</p>
  <p v-if="unvisible">안보임</p>
  <p v-if="visible">난보임</p> -->
  <p v-if="condition === 'A'">A</p>
  <p v-if="condition === 'B'">B</p>
  <p v-if="condition === 'A'">C</p>

  <p v-show="condition">v-show 조건이 참</p>
  <p v-show="!condition">v-show 조건이 거짓</p>

  <ul>
    <li v-for="(name, index) in names">
      index : {{ index }}, value: {{ name }}
    </li>
  </ul>
  <ul>
    <li v-for="name in names">value: {{ name }}</li>
  </ul>
  <ul>
    <li v-for="(name, key) in names">value: {{ name }}, key: {{ key }}</li>
  </ul>

  <h1>user 데이터 출력</h1>
  <ul>
    <li v-for="(item, index) in user" :key="index">
      {{ index }} : {{ item.key }} : {{ item.value }}
    </li>
  </ul>
  <button type="button" v-on:click="clickHandler">버튼</button>
  <button type="button" @dblclick="clickHandler($event)">더블클릭버튼</button>
  <button type="button" @click="($event) => clickHandler($event, 'HelloVue')">
    버튼3
  </button>
</template>
<style>
.red-color {
  color: red;
}
</style>
