<!-- https://github.com/newlxj/stablediffusion-website-online for newlxj -->
<script setup>
import GenerateBtn from '../components/Generate.vue'
import GenerateDialog from '../components/GenerateDialog.vue'
import Album from '../components/Album.vue'
import DialogShowImage from '../components/DialogShowImage.vue'
import Theme from '../components/Theme.vue'
import RandomTagDialog from '../components/RandomTagDialog.vue'
import Login from '../page/Login.vue'

import Go from './Go.vue'
</script>
<template>
  <Login />
  <div class="container">
    <el-header class="header">
      <!-- 头部内容 -->
      <div class="logo-1">
        ai painting
      </div>
    </el-header>
    <el-aside class="aside">
      <!-- 侧边栏内容 -->
      <Theme />
      <Go />
    </el-aside>
    <el-main class="main">
      <!-- 主要内容 -->
      <el-backtop :bottom="100" target=".el-main" :visibility-height="200">
        返回顶部
      </el-backtop>
      <Album />
      <DialogShowImage />
    </el-main>
    <el-footer class="footer">
      <!-- 底部内容 -->
      <el-row :gutter="16">
        <el-col :span="7">
          <el-aside>
            <GenerateBtn />
            <GenerateDialog />
          </el-aside>
        </el-col>
        <el-col :span="7">
          <!-- <el-progress :percentage="processCount" :format="processTabFormat" /> -->
          <el-progress :percentage="processCount" :stroke-width="12" striped striped-flow :duration="duration"
            :format="processTabFormat" color="#e6a23c" />
        </el-col>
        <el-col :span="3" class="versioninfo">
          <!-- 在您不修改、移除以下内容情况下，涉及sdweb-multi-user-website开发的内容可以任意修改使用，有问题请在QQ群：793072950咨询 Begin-->
          <p class="space1">Power By ai8</p>
          <p class="space1"><a href="https://github.com/newlxj/stablediffusion-website-online" target="_blank">github</a> </p>
          <p class="space1"><a href="https://gitee.com/aliu/sdweb-multi-user-website" target="_blank">gitee</a> </p>
          <!-- 在您不修改、移除以上内容情况下，涉及sdweb-multi-user-website开发的内容可以任意修改使用 End-->
        </el-col>
      </el-row>
    </el-footer>
  </div>
  <RandomTagDialog />
</template>


<script>



const processTabFormat = (percentage) => (`还剩${percentage}%图片未浏览`)

export default {
  data() {
    return {
      isCollapse: false,
      processCount: 100,
      duration: 5,
      pageTotal: 100,
      pageSize: 10,
      processTabFormat: processTabFormat,
      page: 1
    };
  },
  mounted: function () {
    this.setPage()
    this.$bus1.on('setPageProgress', (data) => {
      this.processCount = (100 - ((data.pageNum / data.totalSize) * 100)).toFixed(2)
    });
  },
  methods: {
    setPage() {

    },
    handleSelect(index) {
      this.$router.push(index);
    },
  },
};
</script>
<style>
.container {
  position: relative;
}

/******************logo文字效果****************/
.space1 {
  padding-left: 10px
}

.logo-1 {
  color: white;
  animation: neon 3s infinite;

  height: auto;
  text-align: center;
  --shadow-color: #FF9E9E;
  --shadow-color-light: rgba(255, 255, 255, 0.415);
}

.versioninfo {
  display: flex !important;
  justify-content: center !important;
  align-items: center !important;
}
a {
  color: #0066cc; /* 设置超链接颜色 */
  text-decoration: none; /* 去除下划线 */
}

a:hover {
  color: #cc0000; /* 设置鼠标悬停时的颜色 */
}

@keyframes neon {
  0% {
    text-shadow: -1px -1px 1px var(--shadow-color-light), -1px 1px 1px var(--shadow-color-light), 1px -1px 1px var(--shadow-color-light), 1px 1px 1px var(--shadow-color-light),
      0 0 3px var(--shadow-color-light), 0 0 10px var(--shadow-color-light), 0 0 20px var(--shadow-color-light),
      0 0 30px var(--shadow-color), 0 0 40px var(--shadow-color), 0 0 50px var(--shadow-color), 0 0 70px var(--shadow-color), 0 0 100px var(--shadow-color), 0 0 200px var(--shadow-color);
  }

  50% {
    text-shadow: -1px -1px 1px var(--shadow-color-light), -1px 1px 1px var(--shadow-color-light), 1px -1px 1px var(--shadow-color-light), 1px 1px 1px var(--shadow-color-light),
      0 0 5px var(--shadow-color-light), 0 0 15px var(--shadow-color-light), 0 0 25px var(--shadow-color-light),
      0 0 40px var(--shadow-color), 0 0 50px var(--shadow-color), 0 0 60px var(--shadow-color), 0 0 80px var(--shadow-color), 0 0 110px var(--shadow-color), 0 0 210px var(--shadow-color);
  }

  100% {
    text-shadow: -1px -1px 1px var(--shadow-color-light), -1px 1px 1px var(--shadow-color-light), 1px -1px 1px var(--shadow-color-light), 1px 1px 1px var(--shadow-color-light),
      0 0 3px var(--shadow-color-light), 0 0 10px var(--shadow-color-light), 0 0 20px var(--shadow-color-light),
      0 0 30px var(--shadow-color), 0 0 40px var(--shadow-color), 0 0 50px var(--shadow-color), 0 0 70px var(--shadow-color), 0 0 100px var(--shadow-color), 0 0 200px var(--shadow-color);
  }
}

/******************logo文字效果****************/

/* 细滚动条 */
::-webkit-scrollbar {
  width: 5px;
}

/* 滚动槽 */
::-webkit-scrollbar-track {
  background-color: #f5f5f5;
}

/* 滚动条滑块 */
::-webkit-scrollbar-thumb {
  background-color: #ccc;
}

/* 滚动条滑块悬停样式 */
::-webkit-scrollbar-thumb:hover {
  background-color: #999;
}

.el-progress {
  margin-top: 15px;
  margin-bottom: 20px;
  width: 350px;
}

.header {
  text-align: center;
  line-height: 50px;
  background-color: #409EFF;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 50px;
  z-index: 3;
}

.aside {
  position: fixed;
  left: 0;
  top: 50px;
  bottom: 60px;
  /* 头部高度 */
  width: 300px;
  height: 100%;
}

.main {
  overflow-y: auto;
  margin-left: 350px;
  /* 侧边栏宽度 */
  margin-top: 50px;
  /* 头部高度 */
  margin-bottom: 50px;
  /* 底部高度 */
}

.footer {
  background-color: #409EFF;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 50px;
}
</style>
