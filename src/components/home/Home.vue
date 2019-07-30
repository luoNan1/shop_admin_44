<template>
  <!-- 容器 -->
  <el-container>
    <!-- 头部 -->
    <el-header>
      <el-row
        type="flex"
        justify="space-between"
      >
        <el-col :span="6">
          <img
            src="../../assets/logo.png"
            alt=""
          >
        </el-col>
        <el-col :span="6">
          <h1>电商后台管理系统</h1>
        </el-col>
        <el-col
          class="elCol"
          :span="6"
        >
          恭喜上海前端36期月薪2W
          <a
            @click.prevent="logOut"
            href="#"
          >退出</a>
        </el-col>
      </el-row>
    </el-header>
    <!-- 容器 -->
    <el-container>
      <!-- 左侧 -->
      <el-aside width="200px">
        <!--
          el-menu:菜单组件
          el-submenu 子菜单(可以在展开)
          el-menu-item 菜单元素 (最小单位)
          default-active 默认高亮 值是:index

          开启路由模式
          1.给el-moue添加router属性 :router:true
          2.激活时会以index值作为路径进行
         -->
        <el-menu
          :router="true"
          :default-active="handeurlpath()"
          background-color="#545c64"
          text-color="#fff"
          active-text-color="red"
        >
          <!-- one -->
          <el-submenu index="1">
            <!-- 自定义标题 -->
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>用户管理</span>
            </template>
            <!--  -->
            <el-menu-item-group>
              <el-menu-item index="/users">用户列表</el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <!-- two -->
          <el-submenu index="2">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span> 权限管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="/uoles">角色列表</el-menu-item>
              <el-menu-item index="/rights">权限列表</el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <!-- three -->
        </el-menu>
      </el-aside>
      <!-- 主体 -->
      <el-main>
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>

</template>

<script>
export default {
  methods: {
    logOut () {
      this.$confirm('此操作将永久退出, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        localStorage.removeItem('token')
        this.$message({
          type: 'success',
          message: '退出成功!',
          duration: 800
        })

        this.$router.push('/login')
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消退出',
          duration: 800

        })
      })
    },
    handeurlpath () {
      return this.$route.path
    }
  }
}

</script>

<style scoped lang="less">
.el-container {
  height: 100%;
  // 头部
  .el-header {
    background: #b3c1cd;
    padding: 0;
    h1 {
      line-height: 60px;
      color: aliceblue;
    }
    .elCol {
      line-height: 60px;
      text-align: right;
      padding-right: 30px;
      a {
        color: green;
      }
    }
  }
  // 主体部分
  .el-main {
    background: #eaeef1;
  }

  //左侧
  .el-aside {
    background: #545c64;
  }
}
</style>
