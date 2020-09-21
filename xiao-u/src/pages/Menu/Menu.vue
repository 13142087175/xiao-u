<template>
    <div>
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>菜单管理</el-breadcrumb-item>
        </el-breadcrumb>

        <el-button type="primary" @click="goAdd">添加</el-button>

      <el-table
          :data="tableData"
          style="width: 100%"
          row-key="id"
          border  
          default-expand-all
          :tree-props="{children: 'children', hasChildren: 'hasChildren'}">
    <el-table-column
      prop="id"
      label="菜单编号"
      width="180">
    </el-table-column>
    <el-table-column
      prop="title"
      label="菜单名称"
      width="180">
    </el-table-column>
    <el-table-column
      prop="icon"
      label="菜单图标">
    </el-table-column>
    <el-table-column
      prop="url"
      label="菜单地址"
      width="180">
    </el-table-column>
    <el-table-column
      label="状态">
      <template slot-scope="scope">
      <el-tag>{{scope.row.status | statusFormat}}</el-tag>
      </template>
    </el-table-column>

    <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
        <el-popconfirm
        title="确定要删除吗？" @onConfirm="del">
        <el-button
          size="mini"
          type="danger"
           slot="reference">删除</el-button>
</el-popconfirm>
        
      </template>
    </el-table-column>
  </el-table>
    </div>
</template>

<script>
    export default {
        data() {
      return {
        tableData: []
      }
    },
    mounted() {
      this.$http.get("/menulist",{istree:true}).then(res=>{
        this.tableData = res.data.list
      })
    },
    methods: {
      handleEdit (index, row) {
            console.log(index, row);
            this.$router.push("/menu/edit?id=" + row.id)
        },
        handleDelete (index, row) {
            console.log(index, row);
        },
          goAdd(){
              this.$router.push("/menu/add")
          }
    },
    }
</script>

<style lang="stylus" scoped>

</style>