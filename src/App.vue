<template>
  <div id="app">
    <div :class="['music',pause ? 'music--paused' : 'music--rotate']" ref="musicBtn" @click="clickMusic">
      <audio loop="loop" preload="auto" autoplay="autoplay" hidden id="audio"
             :src="musicUrl">
      </audio>
    </div>
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
      musicUrl: '/backgroundMusic.mp3',
      music: {}, // 背景音乐
      musicInit: false, // 是否初始化音乐
      pause: true,
      sideList: [{
        title: '源代码',
        link: 'https://github.com/jujubefoxx/homepage'
      }]
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.music = document.getElementById("audio");//背景音乐对象
      this.pause = this.music.paused
    })
  },
  components: {
    HelloWorld
  },
  methods: {
    clickMusic() {
      if (this.music.paused) {
        this.pause = false;
        this.music.play();
      } else {
        this.pause = true;
        this.music.pause();
      }
    }
  }
}
</script>

<style lang="scss">
@import "assets/scss/variables";
@import "assets/scss/index";
@import "assets/typo.css";


</style>
