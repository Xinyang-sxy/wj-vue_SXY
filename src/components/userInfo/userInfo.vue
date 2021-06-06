<template>
  <el-container >
    <el-aside style="width: 200px;margin-top: 20px">
      <SideMenu></SideMenu>
    </el-aside>
    <el-main>
      <usertable class="books-area" ref="info"></usertable>
    </el-main>
  </el-container>

</template>


<script>
  import SideMenu from "./SideMenu";
  import Usertable from "./usertable";

    export default {
        name: "userInfo",
      components: {Usertable, SideMenu}
    }
</script>

<style scoped>
  .books-area {
    width: 990px;
    margin-left: auto;
    margin-right: auto;
  }
</style>
