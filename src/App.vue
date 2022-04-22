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


</style>
