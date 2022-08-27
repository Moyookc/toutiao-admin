<template>
  <el-container class="layout-container">
    <el-aside width="200px" class="aside">
        <app-aside class="appaside" />
    </el-aside>
    <el-container>
        <el-header class="header">
          <div>
            <i class="el-icon-menu"></i>
            <span>后台管理系统</span>
          </div>
          <el-dropdown >
            <div class="nav-avatar">
              <img class="avatar" src="http://toutiao-img.itheima.net/FgD5soodTLSkqeFumMhbBnNIyrA3" alt="">
              <span class="el-dropdown-link">
                username<i class="el-icon-arrow-down el-icon--right"></i>
              </span>
            </div>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>个人设置</el-dropdown-item>
              <el-dropdown-item>退出登录</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-header>
        <router-view />
    </el-container>
  </el-container>
</template>

<script>
import AppAside from './components/aside.vue'
import { getUserInfo } from '@/api/user'
export default {
  name: 'LayoutIndex',
  components: {
    AppAside
  },
  props: {},
  data () {
    return {
      User: {}
    }
  },
  computed: {},
  watch: {},
  created () {
    this.getUserProfile()
  },
  mounted () {},
  methods: {
    getUserProfile () {
      getUserInfo().then(res => {
        this.User = res.data.data
        console.log(this.User)
      })
    }
  }
}
</script>

<style scoped lang="less">
.layout-container{
    position: fixed;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
}
.aside {
    background-color: rgb(213, 220, 229);
    .appaside {
        height: 100%;
    }
}
.header {
    background-color: rgb(181, 192, 207);
    display: flex;
    justify-content: space-between;
    align-items: center;
    .nav-avatar {
      display: flex;
      align-items: center;
      .avatar {
        margin: 0 10px;
        height: 40px;
        width: 40px;
        border-radius: 50%;
      }
    }
}
.main {
    background-color: rgb(234, 238, 242);
}
</style>
