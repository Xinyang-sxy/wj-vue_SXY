<template>
  <el-form ref="form" :model="form" label-width="80px">
    <el-form-item label="姓  名">
      <el-input v-model="form.name"></el-input>
    </el-form-item>
    <el-form-item label="用户名">
      <el-input v-model="form.username"></el-input>
    </el-form-item>
    <el-form-item label="手机号">
    <el-input v-model="form.phone"></el-input>
    </el-form-item>
    <el-form-item label="邮  箱">
      <el-input v-model="form.email"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submitForm(form)">保存</el-button>
      <el-button>取消</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
    export default {
        name: "usertable",
      data() {
        return {
          form: {
            name: '',
            username: '',
            phone: '',
            email: '',
          },
        }
      },
      mounted () {
        this.findUser()
      },
      methods:{
        findUser () {
          var _this = this
          this.$axios.get('/userInfo/PersonalInfo').then(resp => {
            if (resp && resp.data.code === 200) {
              _this.form = resp.data.result
              console.log(_this.users.name)
            }
          })
        },
        submitForm(form) {
          this.$confirm('确认修改信息？', '提示', {
            confirmButtonText: '确定',
            cancelButtonText: '取消',
            type: 'warning'
          }).then(() => {
              this.$axios
                .put('/userInfo/changeInfo' , {
                  username: form.username,
                  name: form.name,
                  phone: form.phone,
                  email: form.email}).then(resp => {
                if (resp && resp.data.code === 200) {
                  this.$message({
                    type: 'info',
                    message: resp.data.result
                  })
                  this.findUser ()
                }
              })
            }
          )
        },
      }
    }
</script>

<style scoped>

</style>
