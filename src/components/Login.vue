<template>
  <div class="login">
    <el-row :gutter="20">
        <el-col :span="6" :offset="9">
            <el-card class="box-card">
                <el-form ref="Login" :model="Login" label-width="80px">
                    <el-form-item label="账号">
                        <el-input v-model="Login.account"></el-input>
                    </el-form-item>
                    <el-form-item label="密码">
                        <el-input v-model="Login.password" type="password" auto-complete="off"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary" @click="onLogin">立即登录</el-button>
                        <el-button type="danger" @click="onRegist">注册用户</el-button>
                    </el-form-item>
                </el-form>
            </el-card>
        </el-col>
    </el-row>
  </div>
</template>


<script>
    import Config from '../config.js'

    export default{
        name : 'login',
        data (){
            return{
                Login:{
                    account: null,
                    password: null,
                }
            }
        },
        methods:{
            onLogin(){
                if((this.Login.account === null) || (this.Login.account === '')){
                    this.$message.error('请输入账号！');
                    return;
                }

                if((this.Login.password === null) || (this.Login.password === '')){
                    this.$message.error('请输入密码！');
                    return;
                }

                $.getJSON(Config.Main_URL + '/api/login',this.Login, (result) => {
                    if (result.code == 0) {
                        this.$message('登录成功');
                        $.cookie('user_loginToken', result.data.Token, { expires: 1 });  
                        //跳转到主页页面

                    }else{
                        this.$message.error('登录失败');
                    }

                });
            },
            onRegist(){
                
            }
        }

    }
</script>