<template>
  <form
    class="form"
    action=""
    v-on:submit.prevent="formSubmitHandler"
    method="post"
  >
    <h1 class="form__title" v-if="!form_done">Авторизація на сайті</h1>
    <h1 class="form__title" v-else>Авторизація успішна</h1>

    <div v-if="!form_done" class="form__wrapper">
      <label class="form__label" for="">
        <span class="form__input_title">Логін</span>
        <input
          type="text"
          name="login"
          class="form__input form__login"
        >
      </label>
      <p class="form__error_message" v-if="login.toShort">Допустима кількість символів не менше 6</p>
      <p class="form__error_message" v-if="login.toLong">Допустима кількість символів не більше 20</p>
      <br>

      <label class="form__label" for="">
        <span class="form__input_title">Електронна пошта</span>
        <input
          type="text"
          name="email"
          class="form__input form__email"
          v-model="email.value"
        >
      </label>
      <p class="form__error_message" v-if="email.inCorrect">Невірний формат пошти</p>
      <br>

      <label class="form__label" for="">
        <span class="form__input_title">Пароль</span>
        <input
          type="password"
          name="password"
          class="form__input form__password"
        >
      </label>
      <p class="form__error_message" v-if="password.toShort">Допустима кількість символів не менше 8</p>
      <p class="form__error_message" v-if="password.toLong">Допустима кількість символів не більше 24</p>
      <br>

      <button type="submit" class="form__button">
        Авторизуватися
      </button>
    </div>

    <div class="form__result" v-else>
      <img src="../images/check.svg" alt="" class="form__final_img">
      <a href="https://gioc.kyivcity.gov.ua/">
        <button type="button" class="form__button">
          Перейти на головну
        </button>
      </a>
    </div>
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
    form_done: false,
  }),
  methods: {
    formSubmitHandler(event) {
      const requirements = []
      // validate login
      if (event.target.login.value.length < 6) {
        this.login.toShort = true;
        this.login.toLong = false;
        requirements.push(false)
      } else if (event.target.login.value.length > 20) {
        this.login.toLong = true;
        this.login.toShort = false;
        requirements.push(false)
      } else {
        this.login.toShort = false;
        this.login.toLong = false;
        requirements.push(true)
      }

      // validate email
      const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      if (!re.test(event.target.email.value)) {
        this.email.inCorrect = true;
        requirements.push(false)
      } else {
        this.email.inCorrect = false;
        requirements.push(true)
      }

      //validate password
      if (event.target.password.value.length < 8) {
        this.password.toShort = true;
        this.password.toLong = false;
        requirements.push(false)
      } else if (event.target.password.value.length > 20) {
        this.password.toLong = true;
        this.password.toShort = false;
        requirements.push(false)
      } else {
        this.password.toShort = false;
        this.password.toLong = false;
        requirements.push(true)
      }

      console.log(requirements)
      this.form_done = requirements.every(requirement => requirement)
    },
  },
}
</script>

<style lang="scss">
  @import '../styles/mixins';
  @import '../styles/variables';

  .form {
    margin: 0 auto 0;

    width: 500px;

    @include main_font;
    color: #fff;

    border: 4px solid $main_green;
    border-radius: 30px;
    background-color: #fff;
    &__title {
      display: flex;
      justify-content: center;
      align-items: center;

      width: 100%;
      height: 150px;

      color: $main_green;

      border: 0px solid #fff;
      border-radius: 26px 26px 0 0 ;
      background-color: #fff;
      opacity: 0.95;
    }
    &__wrapper, {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      position: relative;
      z-index: 1;
      padding: 60px 0 20px 0;

      height: 450px;

      border-top: 4px solid $main_green;
      border-left: 2px solid $main_green;
      border-right: 2px solid $main_green;
      border-radius: 26px;
      background-color: $main_grey;
    }
    &__label {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    &__input_title {
      padding: 7px;
      border: 1px solid #fff;
      border-radius: 20px;
    }
    &__input_title,
    &__error_message {
      margin-left: 30px;

      width: 195px;

      white-space: nowrap;
    }
    &__input {
      margin-right: 30px;
      padding: 7px;
      height: 35px;
      border: none;
      border-radius: 20px;
      outline: none;
    }
    &__error_message {
      color: #a3812c;
    }
    &__button {
      align-self: center;

      width: 250px;
      height: 50px;

      @include title_font;
      color: $main_green;

      border: none;
      border-radius: 26px;
      cursor: pointer;

      transition: 300ms;
      &:hover {
        color: #fff;
        background-color: $main_green;
      }
    }
    &__result {
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 50px 0 20px 0;

      border-top: 4px solid $main_green;
      border-left: 2px solid $main_green;
      border-right: 2px solid $main_green;
      border-radius: 26px;
      background-color: $main_grey;
    }
    &__final_img {
      width: 50%;
      margin-bottom: 60px;
    }
  }
</style>
