<template>
  <div class="base">
    <el-container>
      <el-header>
        <h1>渠道商品管理系统</h1>
        <el-button type="success" @click="baseout()">退出按钮</el-button>
      </el-header>
      <el-container class="content">
        <!-- 左侧导航栏 -->
        <el-aside width="200px">
          <el-menu
            default-active="2"  class="el-menu-vertical-demo"
          >
          <!-- 统计 -->
            <el-submenu index="1">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>统计</span>
              </template>
              <el-menu-item-group>
                <el-menu-item index="1-1" @click="$router.push({'name':'fxuser'})">用户分析</el-menu-item>
                <el-menu-item index="1-2" @click="$router.push({'name':'fxorder'})">订单分析</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <!-- 管理 -->
           <el-submenu index="1">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>管理</span>
              </template>
              <el-menu-item-group>
                <el-menu-item index="2-1">用户管理</el-menu-item>
                <el-menu-item index="2-2">商品管理</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
          </el-menu>
        </el-aside>
        <!-- 右侧主体 -->
        <el-main>
            <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>
<script>
export default {
  methods: {
    baseout() {
      // 清楚本地存储中的token
      localStorage.removeItem("houtaitoken");
      this.$router.push({ name: "login" });
    }
  }
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
}
.base {
  background: #ebebec;
}
.content {
  margin-top: 20px;
}
.el-header {
  display: flex;
  justify-content: space-around;
  background: #f7f7f7;
  align-items: center;
}

.el-aside {
  margin: 0 10px;
  height: 100vh;
  background: #f7f7f7;
  overflow: auto;
}

.el-main {
  background: #f7f7f7;
  height: 100vh;
  overflow: auto;
  margin-right: 10px;
}
</style>
