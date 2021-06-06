<template>
  <el-menu
    :default-active="'/index'"
    router
    mode="horizontal"
    background-color="white"
    text-color="#222"
    active-text-color="red"
    style="min-width: 1300px">
    <el-menu-item v-for="(item,i) in navList" :key="i" :index="item.name">
      {{ item.navItem }}
    </el-menu-item>
<!--    <a href="#nowhere" style="color: #222;float: right;padding: 20px;">更多功能</a>-->
<!--    <i class="el-icon-menu" style="float:right;font-size: 45px;color: #222;padding-top: 8px"></i>-->
<!--    <el-avatar> {{store.state.username}} </el-avatar>-->
    <el-tooltip class="item" effect="dark"  placement="top-end" style="float: right">
      <div slot="content">{{userState}}</div>
    <i class="el-icon-switch-button" v-on:click="logout" style="float:right;font-size: 40px;color: #222;padding: 10px"></i>
    </el-tooltip>
    <span style="position: absolute;padding-top: 20px;right: 43%;font-size: 20px;font-weight: bold">White Jotter - Your Mind Palace</span>
<!--    <div style="padding-top: 10px">-->
<!--      <el-avatar style="float:right;font-size: 10px" > {{ username }} </el-avatar>-->
<!--    </div>-->
    <el-submenu index="5" style="float: right">
      <template slot="title">{{ username }}</template>
      <el-menu-item index="/user/userInfo">个人中心</el-menu-item>
      <el-menu-item index="/admin">后台管理</el-menu-item>
      <el-menu-item v-on:click="logout">退出登录</el-menu-item>
    </el-submenu>
  </el-menu>

</template>

<script>
  import store from "../../store";

  export default {
    name: 'NavMenu',
    data () {
      return {
        navList: [
          {name: '/index', navItem: '首页'},
          {name: '/jotter', navItem: '精选文章'},
          {name: '/library', navItem: '图书馆'},
          {name: '/user/userInfo', navItem: '个人中心'}
        ],
        username:'',
        userState:''
      }
    },
    mounted () {
      this.findname()
    },
    methods:{
      logout () {
        var _this = this
        this.$axios.get('/logout').then(resp => {
          if (resp.data.code === 200) {
            // 前后端状态保持一致
            _this.$store.commit('logout')
            _this.$router.replace('/login')
          }
        })
      },
      findname(){
        var _this = this
        this.$axios.get('/userInfo/findName').then(resp => {
          if (resp && resp.data.code === 200) {
            _this.username = resp.data.result
            _this.userState = "退出登录"
          }else {
            _this.username = "未登录"
            _this.userState = '登录'
          }
        })
      }

    }
  }
</script>

<style scoped>
  a{
    text-decoration: none;
  }

  span {
    pointer-events: none;
  }

  .el-icon-switch-button {
    cursor: pointer;
    outline:0;
  }


</style>
