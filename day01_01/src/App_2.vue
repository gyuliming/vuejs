<script>
export default {
  data() {
    return {
      number : 0,
      name : 'ssg',
      age : 20,
      gender : 'male'
    };
  },
  methods: {
    onkeyupHandler(event) {
      if (event.keyCode === 13) {
        console.log('Enter key!');
      }
    },
    increment(){
      this.number++;
    },
  },
};
</script>
<template>
<input type="text" @keyup="($event)=>onkeyupHandler($event)"></input><br></br>
<input type="text" @keyup.enter="onkeyupHandler"></input>
<h1 v-once>{{ number }}</h1>
<h1>{{ number }}</h1>
<button type="button" @click="increment">increment</button>
<div v-memo="[name,gender]">
  <p>이름 : {{ name }} </p>
  <p>성별 : {{ gender }}</p>
  <p>나이 : {{ age }}</p>
</div>
<button @click="name = 'ssg1'">이름 변경</button>
<button @click="gender='female'">성별 변경</button>
<button @click="age = 30">나이 변경</button>
<br></br>
<button @click="name = 'ssg1'">이름 변경</button>
<button @click="age = 30">나이 변경</button>
<button @click="gender='female'">성별 변경</button>

</template>
<style></style>
