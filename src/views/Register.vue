<template>
<div class="reg">
       <div class="reg-box">
         <h1>高校舆情管理系统</h1>
         <el-form
        class="register-form"
        :model="registerForm"
        :rules="registerRules"
        ref="ruleForm"
      >
        <!-- 学号 -->
        <el-form-item  prop="username">
          <el-input placeholder="请输入您的账户" v-model="registerForm.username"></el-input>
        </el-form-item>

        <!-- 密码 -->
        <el-form-item prop="password">
          <el-input placeholder="请输入您的密码" type="password" v-model="registerForm.password"></el-input>
        </el-form-item>

            <!-- 注册按钮 -->
          <el-button
            class="btn"
            type="primary"
            @click="sendRegister()"
            size="small"
          >注册</el-button>

          <div class="go-login" @click="goLogin">已有帐号，去登录</div>
      </el-form>
     </div>
</div>
</template>

<script>

export default {
    name: 'register',
    data() {
        return {

            //双向绑定用户输入的信息
            registerForm: {
                username: '',
                password: '',
                
            },

            //表单验证规则
            registerRules: {

                //帐号验证规则
                username:[
                {required: true, message: '请输入你的帐号',trigger: 'blur'},
                {min: 10, max: 10, trigger: 'blur'}
                ],

                //密码验证规则
                password: [
                    {required: true, message: "请输入密码", trigger: "blur" },
                    {min: 6, max: 15,message: "长度在 6 到 15 个字符", trigger: "blur",},
                ],

               
            },

        }
    },

     methods: {
                //跳转到登陆页面
                goLogin () {
                    this.$router.push("/login");
                },

                //发送注册请求
                sendRegister(){
                    let params = {
                    username: this.registerForm.username,                   
                    password: this.registerForm.password,   
                     password2: this.registerForm.password,        
                    };
                  this.$url
                  .post('user/register/',params)
                  .then((res) => {
                    console.log(res);
                    alert('注册成功')
                    this.$router.push('/login');
                  })
                  .catch((err) => {
                    console.log(err)
                  })
                }
                
                
            },
}
</script>

<style lang="less">
.reg{
     width: 100%;
    height: 100%;
    background-image: url("../assets/img/screen/loginbkg.jpg");
    background-size: 100% 100%;
    background-repeat: no-repeat;
    .reg-box{
        width: 25%;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
        h1{
            text-align: center;
            color: #24E0D2;
            margin-bottom: 20px;
            z-index: 0;
        }
        .el-input__inner{
            border-radius:20px;
            color: #24E0D2;
            border: solid 1px #24E0D2;
            height: 32px;
            background-color: transparent;
        }
        input::-webkit-input-placeholder {
        color: #24E0D2;
        }
        .el-button--primary {
        border-radius:20px;
        width: 100%;
        font-size: 16px;
        background-color:#24e0d327;
        color: #24E0D2
        }
        .go-login{ 
        float: right;
        margin-top: 50px;
        font-size: 15px;
        color: white;
        }
        .go-login:hover{
        cursor: pointer;
        color: #24E0D2;;
        }
    }
}




</style>