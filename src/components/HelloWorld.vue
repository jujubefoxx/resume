<template>
  <article class="container">
    <section class="container-side" id="side">
      <!-- 左栏固定开关 Start -->
      <el-switch
          class="container-side__switch"
          style="display: none;"
          v-model="switchValue">
      </el-switch>
      <!-- 左侧固定开关 End-->
      <!-- 个人肖像 -->
      <section class="container-side__photo">
        <el-avatar :src="avatarUrl">
          <img src="https://cube.elemecdn.com/e/fd/0fc7d20532fdaf769a25683617711png.png"/>
        </el-avatar>
        <h1 class="container-side__photo-name">{{ infoData.name }}</h1>
        <h4 class="container-side__photo-job">{{ infoData.job }} / {{ infoData.address }}</h4>
      </section>
      <!-- 基本信息 -->
      <section class="container-side__profile info-unit">
        <h2>
          <i class="el-icon-user-solid"></i>基本信息</h2>
        <hr/>
        <ul>
          <li>
            <label>个人信息</label>
            <span>{{ infoData.name }} / {{ infoData.sex }} / {{ infoData.age }}岁</span>
          </li>
          <li>
            <label>英语水平</label>
            <span>{{ infoData.english }}</span>
          </li>
        </ul>
      </section>
      <!-- 联系方式 -->
      <section class="container-side__contact info-unit">
        <h2>
          <i class="el-icon-phone"></i>联系方式</h2>
        <hr/>
        <ul>
          <li>
            <label>手机</label>
            <a :href="`tel:${infoData.phone}`" target="_blank">{{ infoData.phone }}</a>
          </li>
          <li>
            <label>邮箱</label>
            <a :href="`mailto:${infoData.email}`" target="_blank">{{ infoData.email }}</a>
          </li>
          <!--          <li>-->
          <!--            <label>个人主页</label>-->
          <!--            <a href="http://0b11111110.com/" target="_blank">0b11111110.com/</a>-->
          <!--          </li>-->
          <li>
            <label>Github</label>
            <a :href="`https://${infoData.github}`" target="_blank">{{ infoData.github }}</a>
          </li>
        </ul>
      </section>
      <!-- 技能点 -->
      <section class="container-side__skill info-unit">
        <h2>
          <i class="fa fa-code" aria-hidden="true"></i>技能点</h2>
        <hr/>
        <ul>
          <li class="container-side__skill-progress" v-for="(item,index) in infoData.skill" :key="index">
            <label>{{ item.alias }}</label>
            <el-progress :percentage="item.value" :show-text="false"></el-progress>
          </li>
        </ul>
      </section>
    </section>
  </article>
</template>

<script>
import avatar from "@/assets/images/avatar.jpeg";

export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
      switchValue: false,
      infoData: {
        name: '名字',
        job: '工作',
        address: '地址',
        sex: '女',
        age: '22',
        english: 'CET-4',
        github: 'github.com/jujubefoxx',
        phone: '13631945290',
        email: '905141352@qq.com',
        skill: [
          {alias: 'HTML', value: '90'},
          {alias: 'CSS', value: '90'},
          {alias: 'JavaScript', value: '85'},
          {alias: 'Vue', value: '85'},
          {alias: '小程序', value: '85'},
        ]
      },
      avatarUrl: avatar,
      photoLoading: false,
    }
  },
  methods: {}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "src/assets/scss/variables";
@import "src/assets/scss/reset";
@import "src/assets/scss/index";

@media (min-width: 750px) {
  .container {
    &-side {
      &__switch {
        position: relative;
        display: inline-block !important;
        width: 60px;
        height: 34px;
      }
    }
  }
}

</style>
