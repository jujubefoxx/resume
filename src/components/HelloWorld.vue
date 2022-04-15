<template>
  <article class="container">
    <section class="container-side" id="side">
      <!-- 左栏固定开关-->
      <el-switch
          class="container-side__switch"
          style="display: none;"
          v-model="switchValue">
      </el-switch>

      <!-- 个人肖像 -->
      <section class="container-side__photo">
        <el-avatar :src="infoData.avatar">
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
          <li>
            <label>英语水平</label>
            <span>{{ infoData.english }}</span>
          </li>
          <li>
            <label>计算机水平</label>
            <span>{{ infoData.computer }}</span>
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
      <!-- 二维码 -->
      <section class="container-side__qrcode info-unit">
        <h2><i class="container-icon el-icon-chat-round" aria-hidden="true"></i>微信二维码</h2>
        <hr/>
        <img :src="infoData.qrcode" style="width: 100%;" alt="">
      </section>
    </section>
    <section class="container-main">

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
            <p v-for="(list,key) in item.other" :key="key">{{ list.title }}
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
              <li v-for="(list,key) in item.detailList" :key="key" v-html="list.html">
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
          <li>
            <h3>
              <span>[项目1]医学科学数据管理与共享平台</span>
              <span class="link">
                                <a href="#" target="_blank">Demo</a>
                            </span>
              <time>201X.X-201X.X</time>
            </h3>
            <ul class="info-content">
              <li>技术栈：ThinkPHP+MongoDB+Axure</li>
              <li>
                <i class="container-icon fa-paper-plane-o" aria-hidden="true"></i>
                [目标]实现多类型多来源医学科学数据的提交、管理和共享
                <br/>
                <i class="container-icon fa-users" aria-hidden="true"></i>
                [团队]同 2 位同专业同学一起
                <br/>
                <i class="container-icon fa-bars" aria-hidden="true"></i>
                [贡献]完成从
                <mark>“调研-设计-实现-文档”</mark>
                等工作，主要负责系统原型、功能框架及数据提交流程、元数据及源数据的管理与共享方案的设计以及系统开发等工作
                <br/>
                <i class="container-icon fa-thumbs-o-up" aria-hidden="true"></i>
                [效果]作品最终取得第三届共享杯国家级竞赛“一等奖” （2/2000）
              </li>
            </ul>
          </li>
          <li>
            <h3>
              <span>[项目2]肿瘤流行病数据可视化</span>
              <span class="link">
                                <a href="#" target="_blank">Demo</a>
                            </span>
              <time>201X.X-201X.X</time>
            </h3>
            <ul class="info-content">
              <li>技术栈：HTML 5+D3.js+ECharts+MySQL</li>
              <li>
                <i class="container-icon fa-paper-plane-o" aria-hidden="true"></i>
                [目标]实现常见肿瘤流行病数据多维度可视化展示、数据透视及分析
                <br/>
                <i class="container-icon fa-users" aria-hidden="true"></i>
                [团队]与 1 位同学
                <br/>
                <i class="container-icon fa-bars" aria-hidden="true"></i>
                [贡献]分析项目需求，清洗并整理相关数据(扩展第三方知识组织系统和 Google trends 数据)，并用
                <mark>D3.js</mark>
                和
                <mark>ECharts</mark>
                进行图形化展示以及实现简易自动分析 功能
                <br/>
                <i class="container-icon fa-thumbs-o-up" aria-hidden="true"></i>
                [效果]作品取得第二届共享杯国家级竞赛“特等奖”(1/1500)
              </li>
            </ul>
          </li>
          <li>
            <h3>
              <span>[项目3]肿瘤流行病数据可视化</span>
              <span class="link">
                                <a href="#" target="_blank">Demo</a>
                            </span>
              <time>201X.X-201X.X</time>
            </h3>
            <ul class="info-content">
              <li>技术栈：HTML 5+D3.js+ECharts+MySQL</li>
              <li>
                <i class="container-icon fa-paper-plane-o" aria-hidden="true"></i>
                [目标]实现常见肿瘤流行病数据多维度可视化展示、数据透视及分析
                <br/>
                <i class="container-icon fa-users" aria-hidden="true"></i>
                [团队]与 1 位同学
                <br/>
                <i class="container-icon fa-bars" aria-hidden="true"></i>
                [贡献]分析项目需求，清洗并整理相关数据(扩展第三方知识组织系统和 Google trends 数据)，并用
                <mark>D3.js</mark>
                和
                <mark>ECharts</mark>
                进行图形化展示以及实现简易自动分析功能
                <br/>
                <i class="container-icon fa-thumbs-o-up" aria-hidden="true"></i>
                [效果]作品取得第二届共享杯国家级竞赛“特等奖”(1/1500)
              </li>
            </ul>
          </li>
          <li>
            <h3>
              <span>[项目4]肿瘤流行病数据可视化</span>
              <span class="link">
                                <a href="#" target="_blank">Demo</a>
                            </span>
              <time>201X.X-201X.X</time>
            </h3>
            <ul class="info-content">
              <li>技术栈：HTML 5+D3.js+ECharts+MySQL</li>
              <li>
                <i class="container-icon fa-paper-plane-o" aria-hidden="true"></i>
                [目标]实现常见肿瘤流行病数据多维度可视化展示、数据透视及分析
                <br/>
                <i class="container-icon fa-users" aria-hidden="true"></i>
                [团队]与 1 位
                <br/>
                <i class="container-icon fa-bars" aria-hidden="true"></i>
                [贡献]分析项目需求，清洗并整理相关数据(扩展第三方知识组织系统和 Google trends 数据)，并用
                <mark>D3.js</mark>
                和
                <mark>ECharts</mark>
                进行图形化展示以及实现简易自动分析 功能
                <br/>
                <i class="container-icon fa-thumbs-o-up" aria-hidden="true"></i>
                [效果]作品取得第二届共享杯国家级竞赛“特等奖”(1/1500)
              </li>
            </ul>
          </li>

        </ul>
      </section>
    </section>
  </article>
</template>

<script>
import avatar from "@/assets/images/avatar.jpeg";
import qrcode from "@/assets/images/wechat.jpg";

export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
      switchValue: false,
      infoData: {
        name: '名字', // 名字
        job: '工作', // 工作
        address: '地址', // 地址
        sex: '女', // 性别
        age: '22', // 年龄
        english: 'CET-4', // 英语等级
        github: 'github.com/jujubefoxx', // git
        phone: '13631945290', // 电话
        email: '905141352@qq.com', // 邮箱
        computer: '计算机二级', // 计算机等级
        // 技术点
        skill: [
          {alias: 'HTML', value: 90},
          {alias: 'CSS', value: 90},
          {alias: 'JavaScript', value: 85},
          {alias: 'Vue', value: 65},
          {alias: '小程序', value: 85},
        ],
        // 技术栈
        stack: [
          {
            alias: '前端',
            value: 'Vue(Vue-cli+axios+router)、jQuery、uni-app、Taro、SASS、LESS、Ajax、Bootstrap、Laravel(blade)、ElementUI、VantUI、TaroUI、ant-design-vue'
          },
          // {
          //   alias: '后端',
          //   value: ['C语言、PHP、Node.js']
          // },
          {
            alias: '其他',
            value: 'Photoshop、git、C语言、SAI、Excel、普通话(二甲)'
          },
        ],
        qrcode, // 二维码图片
        avatar, // 头像图片
        // 教育经历
        edu: [{
          school: '东莞理工学院 - 电气工程及其自动化专业(本科)',
          time: '2017.9-2021.7',
          other: [
            {title: '相关课程', content: 'C/C++(96)、matlab(98)、PLC编程(88)'},
            {title: '获得奖项', content: '校挑战杯三等奖、互联网大赛银奖'},
            {
              title: '在校经历',
              content: '大一大二期间担任院团委学生会外联部成员、校职协宣传部部长，组织策划过多场校级大型学生活动，连续两年担任校园大型招聘会线上物料制作者及线下活动负责人；大三期间任职学生助理班主任，协助班主任引导新生50余人的班级进行在校期间的学习和活动'
            }]
        }],
        // 工作经历
        experience: [{
          company: '广东源禾智智能科技有限公司',
          job: '前端开发工程师',
          time: '2021.3-2021.9',
          detailList: [{
            html: '深度参与XX项目迭代XX的前端开发工作，独立承担并完成XX、XX、XXXX等功能点的开发，主要维护并修复XX、XX、XX等功能点bug若干。项目采用技术栈<mark>React+React Router+Node.js+SASS</mark>实现<mark>前后端完全分离</mark>',
          }, {
            html: '配合UI和后端，根据产品需求提供H5页面嵌入到后台模板，要求<mark>移动端显示正常</mark>。'
          }, {
            html: '主要参与XXXXXXX的静态页面开发工作，要求<mark>在支付宝环境下完全兼容</mark>。'
          }],
        },
          {
            company: '广东极速网络科技有限公司',
            job: '前端开发工程师',
            time: '2021.9-至今',
            detailList: [{
              html: '深度参与公司主线产品「XXXX」的前端开发工作，完成帖子快捷回复、<mark>全站图片懒加载</mark>、活动banner、帖子管理（使用Yii框架）等功能。项目采用技术栈phpWind+NAMP。'
            }, {
              html: '配合UI和后端，根据产品需求提供H5页面嵌入到后台模板，要求<mark>移动端显示正常</mark>。'
            }, {
              html: '主要参与XXXXXXX的静态页面开发工作，要求<mark>在支付宝环境下完全兼容</mark>。'
            }],
          }]
      },
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
