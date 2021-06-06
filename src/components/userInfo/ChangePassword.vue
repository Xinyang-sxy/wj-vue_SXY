<template>
  <el-container >
    <el-aside style="width: 200px;margin-top: 20px">
      <side-menu  ref="sideMenu"></side-menu>
    </el-aside>
    <el-main>
      <password-change class="books-area" ref="info"></password-change>
    </el-main>
  </el-container>

</template>

<script>
    import PasswordChange from "./passwordChange";
    import SideMenu from "./SideMenu";
    export default {
        name: "ChangePassword",
      components: {SideMenu, PasswordChange}
    }
</script>

<style scoped>
  .books-area {
    width: 990px;
    margin-left: auto;
    margin-right: auto;
  }
</style>
