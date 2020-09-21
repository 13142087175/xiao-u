<template>
    <el-col :span="24">
      <el-menu default-active="2"
      class="el-menu-vertical-demo"
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b">
      <el-menu-item index="0">
        <i class="el-icon-menu"></i>
        <span slot="title">首页</span>
      </el-menu-item>
      <el-submenu index="1">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span>系统设置</span>
        </template>
          <el-menu-item index="1-1">菜单管理</el-menu-item>
          <el-menu-item index="1-2">角色管理</el-menu-item>
          <el-menu-item index="1-2">管理员管理</el-menu-item>
      </el-submenu>

      <el-submenu index="2">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span>商城设置</span>
        </template>
          <el-menu-item index="2-1">菜单管理</el-menu-item>
          <el-menu-item index="2-2">角色管理</el-menu-item>
          <el-menu-item index="2-2">管理员管理</el-menu-item>
      </el-submenu>
      
      <!-- <el-breadcrumb separator-class="el-icon-arrow-right"> -->
  
    </el-menu>
  </el-col>
</template>

<script>
    export default {
        
    }
</script>

<style lang="stylus" scoped>

</style>