<template>
  <form
    class="form"
    action=""
    v-on:submit.prevent="formSubmitHandler"
  >
    <h1 class="form__title">Авторизація на сайті</h1>

    <label class="form__label" for="">
      <span>Логін</span>
      <input
        type="text"
        name="login"
        class="form__login"
      >
    </label>
    <p v-if="login.toShort">Допустима кількість символів не менше 6</p>
    <p v-if="login.toLong">Допустима кількість символів не більше 20</p>
    <br>

    <label class="form__label" for="">
      <span>Електронна пошта</span>
      <input
        type="text"
        name="email"
        class="form__email"
        v-model="email.value"
      >
    </label>
    <p v-if="email.inCorrect">Невірний формат пошти</p>
    <br>

    <label class="form__label" for="">
      <span>Пароль</span>
      <input
        type="password"
        name="password"
        class="form__password"
      >
    </label>
    <p v-if="password.toShort">Допустима кількість символів не менше 8</p>
    <p v-if="password.toLong">Допустима кількість символів не більше 24</p>
    <br>

    <button type="submit">Авторизуватися</button>
  </form>
</template>

<script>

export default {
  name: 'Form',
  data: () => ({
    login: {
      value: '',
      inCorrect: false,
      toShort: false,
      toLong: false,
    },
    email: {
      value: '',
      inCorrect: false,
    },
    password: {
      value: '',
      inCorrect: false,
      toShort: false,
      toLong: false,
    },
  }),
  methods: {
    formSubmitHandler(event) {
      // validate login
      if (event.target.login.value.length < 8) {
        this.login.toShort = true;
        this.login.toLong = false;
      } else if (event.target.login.value.length > 20) {
        this.login.toLong = true;
        this.login.toShort = false;
      } else {
        this.login.toShort = false;
        this.login.toLong = false;
      }

      // validate email
      const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      if (re.test(event.target.email.value)) {
        this.email.inCorrect = false;
      } else {
        this.email.inCorrect = true;
      }

      //validate password
      if (event.target.password.value.length < 8) {
        this.password.toShort = true;
        this.password.toLong = false;
      } else if (event.target.password.value.length > 20) {
        this.password.toLong = true;
        this.password.toShort = false;
      } else {
        this.password.toShort = false;
        this.password.toLong = false;
      }
    },
  },
}
</script>

<style lang="scss">
  @import '../styles/mixins';
  @import '../styles/variables';

  .form {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin: 0 auto 0;

    width: 40%;
    height: 60vh;

    @include main_font;
    color: #fff;

    border: 4px solid $main_green;
    border-radius: 30px;
    background-color: $main_grey_back;
    &__title {
      position: relative;

      width: 100%;
      height: 30%;

      color: $main_green;

      border: 0px solid #fff;
      border-radius: 26px 26px 0 0 ;
      background-color: #fff;
      opacity: 0.95;
    }
    &__label {
      display: flex;
      justify-content: space-between;
      align-items: center;

      &:first-of-type {
        border-top: 4px solid $main_green;
        border-radius: 26px 26px 0 0 ;
      }
    }
  }
</style>
