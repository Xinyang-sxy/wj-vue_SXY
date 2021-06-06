<template>
  <el-card class="admin-header">
    <el-tooltip class="item" effect="dark" content="返回首页" placement="top-end" style="float: left">
    <a href="/index">
      <img src="../../assets/img/icon/icon2.png" alt="" width="55px" style="float: left;margin-top: -5px;">
    </a>
    </el-tooltip>
    <span style="font-size: 32px;font-weight: bold;position:absolute;left: 100px">后台管理</span>
    <el-tooltip class="item" effect="dark" content="退出登录" placement="top-end" style="float: right">
    <i class="el-icon-switch-button" v-on:click="logout" style="font-size: 40px;float: right"></i>
    </el-tooltip>
  </el-card>
</template>

<script>
  import {createRouter} from '../../router'

  export default {
    name: 'Header',
    methods: {
      logout () {
        var _this = this
        this.$axios.get('/logout').then(resp => {
          if (resp && resp.data.code === 200) {
            _this.$store.commit('logout')
            _this.$router.replace('/index')
            // 清空路由，防止路由重复加载
            const newRouter = createRouter()
            _this.$router.matcher = newRouter.matcher
          }
        }).catch(failResponse => {})
      }
    }
  }
</script>

<style scoped>
  .admin-header {
    height: 80px;
    opacity: 0.85;
    line-height: 40px;
    min-width: 900px;
  }
  .el-icon-switch-button {
    cursor: pointer;
    outline:0;
  }
</style>
