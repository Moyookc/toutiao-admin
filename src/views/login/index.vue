<template>
  <div class="body">
      <div class="login-container">
          <el-form ref="login-form" :model="user" :rules="rules">
              <el-form-item prop="mobile">
                  <el-input v-model="user.mobile" placeholder="请输入手机号"></el-input>
              </el-form-item>
              <el-form-item prop="code">
                  <el-input v-model="user.code" placeholder="请输入密码"></el-input>
              </el-form-item>
              <el-form-item prop="xieyi">
                  <el-checkbox v-model="user.xieyi">我已阅读并同意用户协议和隐私条款</el-checkbox>
              </el-form-item>
              <el-form-item>
                  <el-button
                  class="login-btn"
                  type="primary"
                  @click="onSubmit"
                  :loading="btnloading">登录</el-button>
            </el-form-item>
          </el-form>
      </div>
  </div>
</template>

<script>
import { login } from '@/api/user'
export default {
  name: 'LoginIndex',
  components: {},
  props: {},
  data () {
    return {
      user: {
        mobile: '13911111111',
        code: '246810',
        xieyi: false
      },
      rules: {
        mobile: [
          { required: true, message: '请输入手机号', trigger: 'change' },
          { pattern: /^1[3|5|7|8|9]\d{9}$/, message: '请输入正确的号码格式', trigger: 'change' }
        ],
        code: [
          { required: true, message: '验证码不能为空', trigger: 'change' },
          { pattern: /^\d{6}$/, message: '请输入正确的验证码格式' }
        ],
        xieyi: [
          {
            validator: (rule, value, callback) => {
              if (value) {
                callback()
              } else {
                callback(new Error('请同意用户协议'))
              }
            },
            trigger: 'change'
          }
        ]
      },
      btnloading: false
    }
  },
  methods: {
    onSubmit () {
      this.$refs['login-form'].validate((valid) => {
        if (!valid) {
          return
        }

        // 验证通过，请求登录
        this.login()
      })
    },
    login () {
      const user = this.user
      this.btnloading = true
      login(user)
        .then((res) => {
          this.$message({
            message: '登录成功',
            type: 'success'
          })
          this.btnloading = false
          this.$router.push({
            name: 'home'
          })
        })
        .catch((res) => {
          this.$message.error('登录失败，手机号或验证码错误')
          this.btnloading = false
        })
    }
  }
}
</script>

<style scoped lang="less">
.body {
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  .login-container {
    border: 1px solid rgb(198, 188, 188);
    padding: 50px;
    min-width: 300px;
    .login-btn {
      width: 100%;
    }
  }
}
</style>
