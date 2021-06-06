<template>
  <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
    <el-form-item label="新密码" prop="pass">
      <el-input type="password" v-model="ruleForm.pass" autocomplete="off" show-password></el-input>
    </el-form-item>
    <el-form-item label="确认密码" prop="checkPass">
      <el-input type="password" v-model="ruleForm.checkPass" autocomplete="off" show-password></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submitForm(ruleForm.checkPass)">提交</el-button>
      <el-button @click="resetForm('ruleForm')">重置</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
    import router from "../../router";

    export default {
        name: "passwordChange",
      data() {
        var validatePass = (rule, value, callback) => {
          if (value === '') {
            callback(new Error('请输入密码'));
          } else {
            if (this.ruleForm.checkPass !== '') {
              this.$refs.ruleForm.validateField('checkPass');
            }
            callback();
          }
        };
        var validatePass2 = (rule, value, callback) => {
          if (value === '') {
            callback(new Error('请再次输入密码'));
          } else if (value !== this.ruleForm.pass) {
            callback(new Error('两次输入密码不一致!'));
          } else {
            callback();
          }
        };
        return {
          ruleForm: {
            pass: '',
            checkPass: '',
          },
          rules: {
            pass: [
              { validator: validatePass, trigger: 'blur' }
            ],
            checkPass: [
              { validator: validatePass2, trigger: 'blur' }
            ]
          }
        };
      },
      methods: {
        submitForm(password) {
          this.$confirm('确认修改密码？', '提示', {
            confirmButtonText: '确定',
            cancelButtonText: '取消',
            type: 'warning'
          }).then(() => {
              this.$axios
                .put('/userInfo/changePasswordSubmit/' + password).then(resp => {
                if (resp && resp.data.code === 200) {
                  this.$message({
                    type: 'info',
                    message: resp.data
                  })
                  this.logout ()
                }
              })
              //console.log(password)
            }
          )
        },
        resetForm(formName) {
          this.$refs[formName].resetFields();
        },
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
      }
    }
</script>

<style scoped>

</style>
