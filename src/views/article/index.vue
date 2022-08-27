<template>
  <div class="article-container">
    <div class="top-context">
        <div class="top-header">
            <el-breadcrumb separator-class="el-icon-arrow-right" style="margin-left:20px">
                <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
                <el-breadcrumb-item>内容管理</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="top-main"></div>
    </div>
    <div class="bottom-context"></div>
  </div>
</template>

<script>
export default {
  name: 'ArticleIndex',
  components: {},
  props: {},
  data () {
    return {}
  },
  computed: {},
  watch: {},
  created () {},
  mounted () {},
  methods: {}
}
</script>

<style scoped lang="less">
.article-container {
    margin: 20px;
    .top-context {
        height: 300px;
        border: 1px solid #eceef4;
        box-shadow: #eceef4 10px 10px 10px 5px;
        .top-header {
            display: flex;
            align-items: center;
            height: 50px;
            border-bottom:1px solid #eceef4 ;
        }
    }
}
</style>
