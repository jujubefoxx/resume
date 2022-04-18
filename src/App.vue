<template>
  <div id="app">
    <HelloWorld/>
    <!-- 侧栏 -->
    <aside>
      <ul>
        <li v-for="(item,index) in sideList" :key="index">
          <a :href="item.link" target="_blank">{{ item.title }}</a>
        </li>
      </ul>
    </aside>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data() {
    return {
      sideList: [{
        title: '源代码',
        link: 'https://github.com/jujubefoxx/homepage'
      }]
    }
  },
  components: {
    HelloWorld
  }
}
</script>

<style lang="scss">
@import "assets/scss/variables";
@import "assets/scss/index";
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
