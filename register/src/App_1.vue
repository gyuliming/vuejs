<script>
export default {
  data() {
    return {
      // name: '',
      // email: '',
      // password: '',
      // passwordConfirm: '',
      // nameError: '',
      // emailError: '',
      // pwError: '',
      // pwNotMatchMsg: '',
      user: {
        name: '',
        email: '',
        password: '',
        passwordConfirm: '',
      },
      msg: {
        nameError: '',
        emailError: '',
        pwError: '',
        pwNotMatchMsg: '',
      },
    };
  },
  computed: {
    isValid() {
      return (
        this.user.name.length >= 2 &&
        /^[가-힣a-zA-Z]+$/.test(this.user.name) &&
        /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.user.email) &&
        this.user.password.length > 7 &&
        this.user.passwordConfirm.length > 7 &&
        this.user.password === this.user.passwordConfirm
      );
    },
  },
  watch: {
    // 깊은 방식으로 수정
    // name(newValue, oldValue) {
    //   console.log('oldName : ', oldValue);
    //   console.log('newName : ', newValue);
    //   if (newValue.length < 2) {
    //     this.nameError = '이름은 2글자 이상이어야 합니다';
    //   } else {
    //     this.nameError = '';
    //   }
    'user.name': {
      handler(newValue) {
        // console.log('newName : ', newValue);
        if (newValue.length < 2) {
          this.msg.nameError = '이름은 2글자 이상이어야 합니다';
        } else if (!/^[가-힣a-zA-Z]+$/.test(newValue)) {
          this.msg.nameError = '이름은 한글 또는 영문만 입력 가능합니다';
        } else {
          this.msg.nameError = '';
        }
      },
      deep: true,
    },
    'user.email': {
      handler(newValue) {
        // console.log('newEmail : ', newValue);
        if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(newValue)) {
          this.msg.emailError = '올바른 이메일 형식이 아닙니다.';
        } else {
          this.msg.emailError = '';
        }
      },
      deep: true,
    },
    'user.password': {
      handler(newValue) {
        // console.log('newPassword : ', newValue);
        if (newValue.length < 8) {
          this.msg.pwError = '비밀번호는 8글자 이상이어야 합니다.';
        } else {
          this.msg.pwError = '';
        }
      },
      deep: true,
    },
    'user.passwordConfirm': {
      handler(newValue) {
        if (newValue !== this.user.password) {
          this.msg.pwNotMatchMsg = '비밀번호가 일치하지 않습니다.';
        } else {
          this.msg.pwNotMatchMsg = '';
        }
      },
      deep: true,
    },
  },
  methods: {
    register() {
      if (!this.isValid) {
        return;
      }

      alert(`
      \n이름: ${this.user.name}
      \n이메일: ${this.user.email}
      \n비밀번호: ${this.user.password}
      \n비밀번호 확인: ${this.user.passwordConfirm}`);

      //  clear()

      // 폼 초기화
      this.user.name = '';
      this.user.email = '';
      this.user.password = '';
      this.user.passwordConfirm = '';

      // 에러 메시지 초기화
      this.msg.nameError = '';
      this.msg.emailError = '';
      this.msg.pwError = '';
      this.msg.pwNotMatchMsg = '';
    },
  },
};
</script>
<template>
  <div>
    <form name="forms">
      <label class="form-label">이름 : </label>
      <input v-model="user.name" type="text" name="name" /><br />
      <span class="error">{{ msg.nameError }}</span
      ><br />
      <label class="form-label">이메일 : </label>
      <input v-model="user.email" type="text" name="email" /><br />
      <span class="error">{{ msg.emailError }}</span
      ><br />
      <label class="form-label">비밀번호 : </label>
      <input v-model="user.password" type="password" name="password" /><br />
      <span class="error">{{ msg.pwError }}</span
      ><br />
      <label class="form-label">비밀번호 확인 : </label>
      <input
        v-model="user.passwordConfirm"
        type="password"
        name="passwordConfirm"
      /><br />
      <span class="error">{{ msg.pwNotMatchMsg }}</span>
      <br />
      <input
        type="button"
        value="register"
        @click="register"
        :disabled="!isValid"
      />
    </form>
  </div>
</template>
<style>
.form-label {
  display: inline-block;
  width: 110px;
  text-align: left;
}
.error {
  color: red;
}
</style>
