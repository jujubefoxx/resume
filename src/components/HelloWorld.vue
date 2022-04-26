<template>
  <article class="container">
    <section :class="['container-side','animate__animated','animate__fadeInLeft',switchValue?'container-side--fixed':'']"
             id="side">
      <!-- 左栏固定开关-->
      <el-switch
          class="container-side__switch"
          style="display: none;"
          v-model="switchValue">
      </el-switch>

      <!-- 个人肖像 -->
      <section class="container-side__photo">
        <el-avatar :src="infoData.avatar" class="rotate-avatar">
          <img src="https://cube.elemecdn.com/e/fd/0fc7d20532fdaf769a25683617711png.png"/>
        </el-avatar>
        <h1 class="container-side__photo-name">{{ infoData.name }}</h1>
        <h4 class="container-side__photo-job">{{ infoData.job }} / {{ infoData.address }}</h4>
      </section>
      <!-- 基本信息 -->
      <section class="container-side__profile info-unit">
        <h2>
          <i class="container-icon el-icon-user-solid"></i>基本信息</h2>
        <hr/>
        <ul>
          <li>
            <label>个人信息</label>
            <span>{{ infoData.name }} / {{ infoData.sex }} / {{ infoData.age }}岁</span>
          </li>
          <li v-for="(item,index) in infoData.level" :key="index">
            <label>{{ item.title }}</label>
            <span>{{ item.level }}</span>
          </li>
        </ul>
      </section>
      <!-- 联系方式 -->
      <section class="container-side__contact info-unit">
        <h2>
          <i class="container-icon el-icon-phone"></i>联系方式</h2>
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
          <i class="container-icon el-icon-s-opportunity" aria-hidden="true"></i>技能点</h2>
        <hr/>
        <ul>
          <li class="container-side__skill-progress" v-for="(item,index) in infoData.skill" :key="index">
            <label>{{ item.alias }}</label>
            <el-progress :percentage="item.value" :show-text="false"></el-progress>
          </li>
        </ul>
      </section>
      <!-- 技术栈 -->
      <div class="container-side__stack info-unit">
        <h2><i class="container-icon el-icon-more" aria-hidden="true"></i>其他</h2>
        <hr/>
        <ul>
          <li v-for="(item,index) in infoData.stack" :key="index">
            <label>{{ item.alias }}</label>
            <span>{{ item.value }}</span>
          </li>
        </ul>
      </div>

    </section>
    <section class="container-main animate__animated animate__fadeInRight">
      <!-- 教育经历 -->
      <section class="container-main__edu info-unit">
        <h2>
          <i class="container-icon el-icon-office-building" aria-hidden="true"></i>教育经历</h2>
        <hr/>
        <ul>
          <li v-for="(item,index) in infoData.edu" :key="index">
            <h3>
              <span>{{ item.school }}</span>
              <time>{{ item.time }}</time>
            </h3>
            <p v-for="(list,key) in item.other" :key="key">{{ list.title }}：
              {{ list.content }}
            </p>
          </li>
        </ul>
      </section>
      <!-- 工作经历 -->
      <section class="container-main__experience info-unit">
        <h2>
          <i class="container-icon el-icon-suitcase" aria-hidden="true"></i>工作经历</h2>
        <hr/>
        <ul>
          <li v-for="(item,index) in infoData.experience" :key="index">
            <h3>
              <span>[经历{{ index + 1 }}]{{ item.company }}－{{ item.job }}</span>
              <time>{{ item.time }}</time>
            </h3>
            <ul class="container-main__experience-content">
              <li v-for="(list,key) in item.detailList" :key="key">
                <div v-html="list.html"></div>
                <!--项目地址-->
                <div v-if="list.project">
                  项目地址：
                  <a :href="project.url||'javascript:;'" :target="project.url ? '_blank' : '_self'"
                     v-for="(project,i) in list.project"
                     class="container-main__link"
                     :key="i">
                    {{
                      list.project.length > 1 ? `[${i +
                      1}]` : ''
                    }}
                    <i class="container-icon el-icon-link" aria-hidden="true" v-if="project.url"></i>{{ project.title }}</a>
                </div>
                <!--代码片段-->
                <template v-if="list.link">
                  <a :href="link" target="_blank" v-for="(link,num) in list.link" class="container-main__link"
                     :key="num">
                    <i class="container-icon el-icon-link" aria-hidden="true"></i>
                    {{
                      list.link.length > 1 ? `[${num +
                      1}]` : ''
                    }}代码片段</a>
                </template>
              </li>
            </ul>
          </li>
        </ul>
      </section>
      <!-- 项目经验 -->
      <section class="container-main__project info-unit">
        <h2>
          <i class="container-icon el-icon-folder-opened" aria-hidden="true"></i>个人项目</h2>
        <hr/>
        <ul>
          <li v-for="(item,index) in infoData.project" :key="index">
            <h3>
              <span>[项目{{ index + 1 }}]{{ item.title }}</span>
              <template v-if="item.file">
                <a class="container-main__demo" :href="item.file.link" :download="item.file.title">{{
                    item.file.type
                  }}文件</a>
              </template>
              <template v-if="item.demoLink">
              <span class="container-main__demo" v-for="(link,key) in item.demoLink"
                    :key="key">
                <a :href="link" target="_blank">Demo{{ key + 1 }}</a>
              </span>
              </template>
              <time>{{ item.time }}</time>
            </h3>
            <ul class="container-main__content">
              <li>技术栈：{{ item.stack }}</li>
              <li>
                <i class="container-icon el-icon-s-promotion" aria-hidden="true"></i>
                [目标]{{ item.target }}
                <br/>
                <i class="container-icon el-icon-s-custom" aria-hidden="true"></i>
                [团队]{{ item.team }}
                <br/>
                <i class="container-icon el-icon-s-data" aria-hidden="true"></i>
                [贡献]<span v-html="item.contributionHTML"></span>
                <template v-if="item.link">
                  <a :href="link" target="_blank" v-for="(link,num) in item.link" class="container-main__link"
                     :key="num">
                    <i class="container-icon el-icon-link"
                       aria-hidden="true"></i>{{ item.link.length > 1 ? `[${num + 1}]` : '' }}代码片段</a>
                </template>
                <br/>
                <i class="container-icon el-icon-data-analysis" aria-hidden="true" v-if="item.result"></i>
                {{ item.result ? `[效果]${item.result}` : '' }}
              </li>
            </ul>
          </li>
        </ul>
      </section>
      <!-- 自我评价 -->
      <section class="container-main__self info-unit">
        <h2>
          <i class="container-icon el-icon-edit" aria-hidden="true"></i>自我评价/期望</h2>
        <hr/>
        <p>
          {{ infoData.self }}
        </p>
      </section>
      <!-- 二维码 -->
      <section class="container-main__qrcode info-unit">
        <h2><i class="container-icon el-icon-chat-round" aria-hidden="true"></i>二维码</h2>
        <hr/>
        <div class="container-main__qrcode-container">
          <div class="container-main__qrcode-list" v-for="(img,index) in infoData.qrcode" :key="index">
            <img style="width: 100%" :src="img.img" :alt="img.title">
            <span>{{ img.title }}</span>
          </div>
        </div>
      </section>
    </section>
  </article>
</template>

<script>
import avatar from "@/assets/images/avatar.jpeg";
import wechat from "@/assets/images/wechat.png";
import github from "@/assets/images/github.png";

export default {
  name: 'HelloWorld',
  data() {
    return {
      switchValue: false,
      infoData: {
        name: '名字', // 名字
        job: '工作', // 工作
        address: '地址', // 地址
        sex: '女', // 性别
        age: '22', // 年龄
        // 基本等级
        level: [
          {
            title: '英语等级',
            level: 'x级'
          }, {
            title: '计算机等级',
            level: 'x级'
          }],
        github: 'github.com/jujubefoxx', // git
        phone: '1XXXXXXXXXX', // 电话
        email: 'XXXXXXXXXX@XX.com', // 邮箱
        // 技术点
        skill: [
          {alias: 'HTML', value: 90},
          {alias: 'CSS', value: 90},
          {alias: 'JavaScript', value: 85},
          {alias: 'Vue2', value: 65},
          {alias: '小程序', value: 85},
        ],
        // 技术栈
        stack: [
          {
            alias: '前端',
            value: 'jQuery、uni-app、Taro、SASS、LESS、Ajax、Bootstrap、Laravel'
          },
          // {
          //   alias: '后端',
          //   value: ['C语言、PHP、Node.js']
          // },
          {
            alias: '其他',
            value: 'git、C/C++'
          },
        ],
        qrcode: [{title: 'wechat', img: wechat}, {title: 'github', img: github}], // 二维码图片
        avatar, // 头像图片
        // 教育经历
        edu: [{
          school: 'XXXX大学 -XXXXXXXXXX专业(X科)',
          time: '201X.9-202X.7',
          //其他内容
          other: [
            {title: '相关课程', content: 'XX(分数)、XX(分数)'},
            {title: '获得奖项', content: '获得奖项'},
            {
              title: '在校经历',
              content: '……'
            }]
        }],
        // 工作经历
        experience: [
          {
            company: 'XXXXX公司',
            job: '前端开发工程师',
            time: '202X.X-202X.X',
            detailList: [{
              html: '深度参与XXXXXX小程序项目迭代X.0的XX开发工作，独立承担并完成XXXX的开发，分析需求和产品原型图并使用<mark>Vue-cli + element-ui + Axios</mark>进行XXXXX系统开发，主要有<mark>XXXXXXXXXXX功能等若干</mark>，并在后期优化时实现了<mark>自适应</mark>的效果。',
              //代码片段/博客文章
              link: ['www.baidu.com']
            }, {
              html: '配合UI和后端，根据产品需求使用<mark>HTML5 + jquery</mark>提供H5页面完成XXXXX，要求<mark>移动端自适应及显示正常</mark>。',
              project: [
                {title: '极速有料h5', url: 'https://h.jsty.com'}, // 项目地址，（可选）
                {title: '小程序：极速有料(微信、头条、百度、QQ)'}, // 项目地址
                {title: '今天好料官网', url: 'https://hl.tiyipu.com/'}] // 项目地址
            }, {
              html: '配合XXXX进行XXX小程序的页面开发。',
            }],
          }],
        // 项目经历
        project: [{
          title: 'XXXXAPP',
          time: '2021.10-2022.1',
          stack: 'uni-app + uView + spring + mysql + git',
          target: '实现一个集XX、XX、XXX、XXX、XXXX等多功能一体的XXXXAPP',
          team: '与java开发1人',
          contributionHTML: '分析需求使用<mark>Vue-cli+element-ui+Axios</mark>进行后台管理系统开发，功能包括XXXXX等，并根据设计稿使用<mark>uni-app</mark>进行前台APP的开发，实现APP的所有需求功能。',
          // file: {
          //   link: '', // 文件地址 放在public下
          //   type: '', // 文件类型,
          //   title: '' // 文件名
          // }, // 文件(可选)
          // 代码片段(可选)
          link: ['https://blog.csdn.net/lcc0628/article/details/121181318?spm=1001.2014.3001.5502', 'https://blog.csdn.net/lcc0628/article/details/121899565?spm=1001.2014.3001.5502', 'https://blog.csdn.net/lcc0628/article/details/122010197?spm=1001.2014.3001.5502']
        },
          {
            title: '今天吃啥大转盘',
            time: '2022.3-至今',
            stack: 'Vue + Taro3(Vue) + Taro-UI-Vue',
            target: '实现一个能够获取随机结果的大转盘并自主进行配置的转盘，h5端仅有转盘和配置功能，小程序端可以实现查询相关菜谱(持续更新)',
            team: '自己',
            contributionHTML: '使用<mark>Vue</mark>进行H5端的开发，完成转盘和转盘配置功能，后续迁移至小程序端，使用<mark>Taro3(Vue) + Taro-UI-Vue</mark>进行微信小程序端的开发，增加了菜谱功能等。',
            result: '单月新增用户量600人',// 效果(可选)
            demoLink: ['https://github.com/jujubefoxx/Taro_HungryTurntable', 'https://github.com/jujubefoxx/WhatDoWeHaveToEat-'],// demo(可选)
          }],
        //自我评价
        self: '自我评价自我评价自我评价自我评价自我评价',
      },
      photoLoading: false,
    }
  },
  created() {
    console.log("感谢您的浏览，期待能够加入贵公司！")
  },
  methods: {}
}
</script>

<style scoped lang="scss">
@import "src/assets/scss/variables";
@import "../assets/scss/index";
@import "src/assets/scss/article";

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
