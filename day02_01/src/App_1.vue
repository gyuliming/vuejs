<script>
export default {
  data() {
    return {
      firstName: 'Minsu',
      lastName: 'Kim',
      numberArray: [1, 2, 3, 4, 5],
      inputStr: '',
      num: 0,
      arr: [0, 1, 2],
      obj: { name: 'Messi', age: 38 },
    };
  },
  computed: {
    fullName() {
      console.log('computed fullName');
      return `${this.lastName} ${this.firstName}`;
    },
    evenSum() {
      return this.numberArray
        .filter((v) => v % 2 == 0)
        .reduce((acc, cur) => acc + cur, 0);
    },
  },
  watch: {
    inputStr(newValue, oldValue) {
      console.log(`old value : ${oldValue}`);
      console.log(`new value : ${newValue}`);
    },
    num(newValue, oldValue) {
      console.log(`old value : ${oldValue}`);
      console.log(`new value : ${newValue}`);
    },
    arr: {
      handler(newValue, oldValue) {
        console.log(`old value : ${oldValue}`);
        console.log(`new value : ${newValue}`);
      },
      deep: true,
    },
    // obj(newValue, oldValue) {
    //   console.log(`old value : ${oldValue}`);
    //   console.log(`new value : ${newValue}`);
    // },
    obj: {
      handler(newValue, oldValue) {
        console.log(`old value : ${JSON.stringify(oldValue)}`);
        console.log(`new value : ${JSON.stringify(newValue)}`);
      },
      deep: true,
    },
  },
};
</script>
<template>
  <h1>{{ lastName }}-{{ firstName }}</h1>
  <h1>{{ firstName }} - {{ lastName }}</h1>
  <h1>{{ fullName }}</h1>
  <h1>{{ evenSum }}</h1>

  <input type="text" v-model="inputStr" />
  <h1>{{ arr }}</h1>
  <h1>{{ obj }}</h1>

  <button @click="arr.push(3)">배열값 변경</button>
  <br />
  <button @click="obj.name = 'Ronaldo'">객체값 변경</button>
  <br />
  <button @click="obj.age = 25">연령 정보 변경</button>
</template>
<style></style>
