<template>
    <div>
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item :to="{path:'/menu'}">菜单管理</el-breadcrumb-item>
            <el-breadcrumb-item>{{title}}</el-breadcrumb-item>
        </el-breadcrumb>

        <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
            <el-form-item label="菜单名称" prop="title">
                <el-input v-model="ruleForm.title"></el-input>
            </el-form-item>
            <el-form-item label="上级菜单" prop="pid">
                <el-select v-model="ruleForm.pid" placeholder="请选择">
                <el-option label="顶级菜单" :value="0"></el-option>
                <el-option :label="item.title" :value="item.id" 
                            v-for="(item,index) in menuList" :key="item.id"></el-option>
                </el-select>
            </el-form-item>

            <el-form-item label="菜单类型" prop="type">
                <el-radio-group v-model="ruleForm.type">
                <el-radio :label="1">目录</el-radio>
                <el-radio :label="2">菜单</el-radio>
                </el-radio-group>
            </el-form-item>

            <el-form-item label="菜单图标" prop="icon" v-show="ruleForm.type == 1">
                <el-input v-model="ruleForm.icon"></el-input>
            </el-form-item>

            <el-form-item label="菜单地址" prop="url" v-show="ruleForm.type == 2">
                <el-input v-model="ruleForm.url"></el-input>
            </el-form-item>
           
            <el-form-item label="状态" prop="status">
                <el-switch v-model="ruleForm.status"></el-switch>
            </el-form-item>
        
            <el-form-item>
                <el-button type="primary" @click="submitForm('ruleForm')">{{buttonTitle}}</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>

<script>
    export default {
        data() {
      return {
        id:"",
        title:"",
        buttonTitle:"",
        menuList: [],
        ruleForm: {
          title:"",
          pid:"",
          icon:"",
          type:"",
          url:"",
          status:true
        },
        rules: {
          title: [
            { required: true, message: '请输入菜单名称', trigger: 'blur' },
          ],
          pid: [
            { required: true, message: '请选择', trigger: 'change' }
          ]
          
        }
      };
    },

    mounted() {
    this.id = this.$route.query.id
    if(this.id){
       this.title = "菜单编辑"
       this.buttonTitle = "修改"
       this.$http.get("/menuinfo",{id:this.id}).then(res =>{
         let {status} = res.data.list
        this.ruleForm = {...res.data.list, status: status == 1 ? true : false}
       })
    }else{
      this.title = "菜单添加"
       this.buttonTitle = "添加"
    }

    if(this.$route.path == "/role/add"){

    }else if(this.$route.path == "/menu/edit"){

    }
      this.$http.get("/menulist").then(res=>{
        console.log(res)
        this.menulist = res.data.list
      })
    },

    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            this.ruleForm.status = this.ruleForm.status ? 1:2
            if(this.id){
              this.$http.post("/menuedit",{...this.ruleForm,id:this.id}).then(res=>{
                console.log(res)
                if(res.data.code == 200){
                  this.$router.push("/menu")
                }
              })
            }else{
              this.$http.post("/menuadd",this.ruleForm).then(res=>{
                console.log(res)
              })
            }
            
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
    }
</script>

<style lang="stylus" scoped>

</style>