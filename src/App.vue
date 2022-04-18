<template>
  <div id="app">
    <!--    <img alt="Vue logo" src="./assets/logo.png">-->
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style lang="scss">
@import "assets/scss/variables";
@import "assets/scss/reset";
@import "assets/typo.css";

//公共部分
body {
  background: #e5e5e5 url(@/assets/images/background.png);
  width: 100%;
  overflow-x: hidden;
  padding: 1rem 10% 0;
  box-sizing: border-box;
  font-size: .9em;

  .info-unit {
    margin-bottom: 1rem;

    h2 {
      font-weight: 700;
    }

    h3 {
      font-weight: 300;
    }

    .container-icon {
      margin-right: .3em;
    }
  }
}

</style>
