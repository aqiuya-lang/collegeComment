<template>
      <div class="login">
         <div class="login-box">
            <h1>高校舆情管理系统</h1>
            <el-form
            class="login-form"
            :model="loginForm"
            ref="ruleForm"
          >
            <!-- 帐号 -->
            <el-form-item  prop="username">
              <el-input  v-model="loginForm.username" placeholder="请输入你的帐号"></el-input>
            </el-form-item>

            <!-- 密码 -->
            <el-form-item  prop="password">
              <el-input  type="password" v-model="loginForm.password" placeholder="请输入你的密码"></el-input>
            </el-form-item>

            <!-- 点击登录 -->
              <el-button
              class="btn"
                type="primary"
                @click="sendLogin()"
                size="small"
              >登录</el-button>

              <!-- 跳转到登录页面 -->
              <div class="go-reg" @click="goRegister">没有帐号，去注册</div>
          </el-form>    
          </div>
      </div>
</template>

<script>

export default {
  name: 'login',
  data () {
    return {

      //双向绑定用户输入信息
      loginForm:{
        username: '',
        password: ''
      },

      //表单验证规则
      loginRules: {

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

    //跳转到注册页面
    goRegister () {
      this.$router.push("/register")
    },
    
    //发送登录请求
    sendLogin () {
      let params = {
        username: this.loginForm.username,
        password: this.loginForm.password,
       
      }
      this.$url
      .post('user/login/', params)
      .then(res => {
        console.log(res.data.msg)
       alert('登录成功')
        console.log(res);
        this.$router.replace('/home');
      })
      .catch(err => {
        console.log(err)
      })
    }
  }

}
</script>

<style  lang="less">
.login{
  width: 100%;
  height: 100%;
  background-image: url("../assets/img/screen/loginbkg.jpg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
    .login-box{
      width: 25%;
      position: absolute;
      top:50%;
      left:50%;
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
        color: #24E0D2;
        
        }
      .go-reg{ 
      float: right;
      margin-top: 50px;
      font-size: 15px;
      color: white;
      }
      .go-reg:hover{
        cursor: pointer;
        color: #24E0D2;;
      }
    }

}


</style>