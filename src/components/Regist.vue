<template>
  <div id="regist">
    <el-container>
        <el-header>
            <el-row :gutter="20">
                <el-col :span="12" :offset="6">
                    <h2>注册页面</h2>
                </el-col>
            </el-row>
        </el-header>
        <el-main>
            <el-row :gutter="20">
                <el-col :span="12" :offset="6">
                    <el-form :model="Regist" :rules="rules" ref="Regist" label-width="100px" class="demo-ruleForm">
                        <el-form-item label="账号" prop="account">
                            <el-input v-model="Regist.account"></el-input>
                        </el-form-item>
                        <el-form-item label="用户名" prop="username">
                            <el-input v-model="Regist.username"></el-input>
                        </el-form-item>
                        <el-form-item label="密码" prop="password">
                            <el-input v-model="Regist.password" type="password" auto-complete="off"></el-input>
                        </el-form-item>
                        <el-form-item label="确认密码" prop="checkpassword">
                            <el-input v-model="Regist.checkpassword" type="password" auto-complete="off"></el-input>
                        </el-form-item>                   
                        <el-form-item>
                            <el-button type="primary" @click="OnRegist('Regist')">立即创建</el-button>
                            <el-button @click="resetForm('Regist')">重置</el-button>
                        </el-form-item>
                    </el-form>
                </el-col>
            </el-row>
        </el-main>
    </el-container>
  </div>
</template>

<script>
    import Config from '../config.js'

    export default{
        name: 'regist',
        data(){
            return{
                Regist:{
                    account:null,
                    password:null,
                    checkpassword:null,
                    username:null,
                },
                rules: {
                    account: [
                        { required: true, message: '请输入账号', trigger: 'blur' },
                    ],
                    username: [
                        { required: true, message: '请输入用户名', trigger: 'blur' }
                    ],
                    password: [
                        { required: true, message: '请输入密码', trigger: 'blur' }
                    ],
                    checkpassword: [
                        { required: true, message: '再一次输入密码', trigger: 'blur' }
                    ]
                }
            }
        },
        methods:{
            OnRegist(formName){
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        if(this.Regist.password != this.Regist.checkpassword){
                            this.$message.error('请填写正确密码');
                            return false;
                        }

                        //登录
                        $.post(Config.Main_URL + "/api/regist", {
                            'account':this.Regist.account,
                            'password':this.Regist.password,
                            'username':this.Regist.username
                            }, (result) =>{
                            if(result.code == 0){
                                this.$message('添加成功');
                                this.$router.push('/Login');
                            }else{
                                this.$message.error('添加失败');
                            }
                            return true;
                        });
                    } else {
                        this.$message.error('请填写完整信息');
                        return false;
                    }
        });
            },
            resetForm(formName){
                this.$refs[formName].resetFields();
            }
        }
    }
</script>