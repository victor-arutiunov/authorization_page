<template class="template">
  <Form />
</template>

<script>
import Form from './components/Form';

export default {
  name: 'App',
  components: {
    Form,
  },
}
</script>

<style lang="scss">
  @import 'styles/mixins';
  @import 'styles/variables';

  #app {
    padding-top: 70px;

    height: 100vh;

    background-color: $main_grey_back;
    &::before {
      content: " ";
      position: absolute;
      top: 0;
      left: 0;
      z-index: -1;
      width: 100%;
      height: 100%;
      background-image: url('./images/kyiv.jpg');
    }
  }
</style>
