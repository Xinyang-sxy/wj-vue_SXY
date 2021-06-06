<template>
  <el-menu
    class="categories"
    active-text-color="red"
    router>
    <el-menu-item index="/user/userInfo">
      <i class="el-icon-menu"></i>
      <span slot="title">个人信息</span>
    </el-menu-item>
    <el-menu-item index="/user/ChangePassword">
      <i class="el-icon-menu"></i>
      <span slot="title">修改密码</span>
    </el-menu-item>
    <el-menu-item index="#">
      <i class="el-icon-menu"></i>
      <span slot="title">其&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp他</span>
    </el-menu-item>
  </el-menu>
</template>

<script>
    export default {
      name: 'SideMenu',

    }
</script>

<style scoped>
  .categories {
    position: fixed;
    margin-left: 50%;
    left: -600px;
    top: 100px;
    width: 150px;
  }
</style>
