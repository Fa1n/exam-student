<template>
  <el-container>
    <el-header height="61" class="student-header">
<!--      <div class="head-user">
        <el-dropdown trigger="click" placement="bottom">
          <el-badge :is-dot="messageCount!==0" >
            <el-avatar  class="el-dropdown-avatar" size="medium"  :src="require('@/assets/avatar.png')"></el-avatar>
          </el-badge>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item @click.native="$router.push({path:'/user/index'})">个人中心</el-dropdown-item>
            <el-dropdown-item @click.native="$router.push({path:'/user/message'})">
              <el-badge :value="messageCount" v-if="messageCount!==0">
                <span>消息中心</span>
              </el-badge>
              <span  v-if="messageCount===0">消息中心</span>
            </el-dropdown-item>
            <el-dropdown-item @click.native="logout" divided>退出</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </div>
      <el-menu class="el-menu-title" mode="horizontal" :default-active="defaultUrl" :router="true">
        <el-menu-item index="/Test/test">跳转</el-menu-item>
        <el-menu-item index="/index">首页</el-menu-item>
        <el-menu-item index="/paper/index">试卷中心</el-menu-item>
        <el-menu-item index="/record/index">考试记录</el-menu-item>
        <el-menu-item index="/question/index">错题本</el-menu-item>
      </el-menu>-->
      <div class="title1">
        <img src="@/assets/title.png" height="56"/>
        <div class="title" >青岛石化检安学习平台</div>
      </div>
    </el-header>
    <el-main class="student-main">
      <router-view/>
    </el-main>
    <footer class="yks-footer clearfix">
      <div class="bottom-menu">
        <div class="bm-child"  :class="{on: '/Test/test' === $route.path}" @click="goto('/Test/test')">
          <div class="row">
            <i class="iconfont icon-icon-test6"></i>
          </div>
          <div class="row">
            <span>首页</span>
          </div>
        </div>
        <div class="bm-child" :class="{on: '/index' === $route.path}"  @click="goto('/index')">
          <div class="row">
            <i class="iconfont icon-icon-test2"></i>
          </div>
          <div class="row">
            <span>考试</span>
          </div>
        </div>
        <div class="bm-child" :class="{on: '/record/index' === $route.path}" @click="goto('/record/index')">
          <div class="row">
            <i class="iconfont icon-icon-test4"></i>
          </div>
          <div class="row">
            <span>记录</span>
          </div>
        </div>
        <div class="bm-child" :class="{on: '/user/index' === $route.path}" @click="goto('/user/index')">
          <div class="row">
            <i class="iconfont icon-icon-test7"></i>
          </div>
          <div class="row">
            <span>我的</span>
          </div>
        </div>

<!--        <div class="bm-child" @click="switchTo('/home')">
          <img src="https://home.youkaoshi.cn/ustatic/img/student/practice-icon-on.png" alt="">
          <p style="color: rgb(54, 170, 253);">首页</p>
        </div>
        <div class="bm-child" href="/paper/index">
          <img src="https://home.youkaoshi.cn/ustatic/img/student/exam-icon-off.png" alt="">
          <p style="color: rgb(0, 0, 0);">考试</p>
        </div>
        <div class="bm-child" href="">
          <img src="https://home.youkaoshi.cn/ustatic/img/student/study-icon-off.png" alt="">
          <p style="color: rgb(0, 0, 0);">学习</p>
        </div>
        <div class="bm-child" href="">
          <img src="https://home.youkaoshi.cn/ustatic/img/student/myself-icon-off.png" alt="">
          <p style="color: rgb(0, 0, 0);">我的</p>
        </div>-->

      </div>
    </footer>
  </el-container>
</template>
<script>
import { mapActions, mapMutations, mapState } from 'vuex'
import loginApi from '@/api/login'
export default {
  name: 'Layout',
  data () {
    return {
      value1: 0,
      defaultUrl: '/index'
    }
  },
  created () {
    this.defaultUrl = this.routeSelect(this.$route.path)
    this.getUserMessageInfo()
  },
  watch: {
    $route (to, from) {
      this.defaultUrl = this.routeSelect(to.path)
    }
  },
  methods: {
    goto (path) {
      this.$router.replace(path)
    },
    routeSelect (path) {
      let topPath = ['/', '/index', '/paper/index', '/record/index', '/question/index']
      if (topPath.indexOf(path)) {
        return path
      }
      return null
    },
    logout () {
      let _this = this
      loginApi.logout().then(function (result) {
        if (result && result.code === 1) {
          _this.clearLogin()
          _this.$router.push({ path: '/login' })
        }
      })
    },
    ...mapActions('user', ['getUserMessageInfo']),
    ...mapMutations('user', ['clearLogin'])
  },
  computed: {
    ...mapState('user', {
      messageCount: state => state.messageCount
    })
  }
}
</script>

<style lang="scss" scoped>
  .yks-footer {
    position: fixed;
    width: 100%;
    bottom: 0;
    padding-left: 0;
    padding-right: 0;
    clear: both;
    z-index: 3;
    margin-bottom: 0;
    background-color: #fff;
  }

  .bottom-menu {
    display: flex;
    width: 100%;
    height: 60px;
    -webkit-box-shadow: 0 2px 6px 0 rgba(7, 17, 27, .5);
    -moz-box-shadow: 0 2px 6px 0 rgba(7, 17, 27, .5);
    -o-box-shadow: 0 2px 6px 0 rgba(7, 17, 27, .5);
    box-shadow: 0 2px 6px 0 rgba(7, 17, 27, .5);
    -moz-transition: .3s -moz-box-shadow linear;
    -webkit-transition: .3s -webkit-box-shadow linear;
    -o-transition: .3s -webkit-box-shadow linear;
    transition: .3s box-shadow linear;
  }

  .bottom-menu .bm-child {
    display: block;
    flex: 1;
    height: 50px;
    text-align: center;
    cursor: pointer;
  }

  .bottom-menu .bm-child img {
    width: 27px;
    margin-top: 2px;
  }
  .demo-carousel{
    color: #475669;
    font-size: 14px;
    opacity: 0.75;
    line-height: 150px;
    margin: 0;
  }

  .tab-bar {
    background-color: white;
    height: 54px;
    border: 0 solid rgb(210, 210, 210);
    border-top-width: 1px;
    position: fixed;
    margin: auto;
    bottom: 0;
    width: 100%;
  }

  .tab-bar-item {
    height: 54px;
  }

  i {
    font-size: 25px;
  }
  .on {
    color: #1E90FF;
  }
  .title1{
    width: 100%;
    height: 56px;
    overflow: hidden;
  }
  .title1 img{
    float: left;
  }
  .title{
    margin-left: 10px;
    font-size: 20px;
    font-weight:bold;
    line-height: 85px;
    font-family:"微软雅黑";
  }
</style>
