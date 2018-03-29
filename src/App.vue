<template lang="pug">
  #app
    .container
      todo
</template>

<script>
import todo from "./components/todo";

export default {
  components: {
    todo
  },
  name: 'app',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App'
    };
  }
};
</script> 

<style lang="scss" src="" scoped></style>
