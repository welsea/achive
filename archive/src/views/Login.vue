<template>
  <div class="login">
    <div class="input">
      <h1>Welcome to Archive</h1>
      <el-input placeholder="请输入ID" v-model="input" clearable style="width:200px;margin-bottom:1em">
      </el-input>
      <el-input placeholder="请输入密码" v-model="pw" show-password clearable style="width:200px;margin-bottom:1em">
      </el-input>
      <el-button type="primary" style="width:200px" @click="login">登录</el-button>
    </div>
    <div class="contact">
      <el-tooltip class="item" effect="light" content="请联系sxy.42@outlook.com" placement="top-end">
        <el-button class="contact-show"><i class="el-icon-question"></i>
          帮助</el-button>
      </el-tooltip>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'Login',
    data() {
      return {
        input: '',
        pw: ''
      }
    },
    components: {

    },
    methods: {
      login() {
        //登录函数
        this.$router.push('/home')
      }
    }
  }
</script>
<style scoped>
  h1 {
    font-size: 3em;

  }

  .login::before {
    content: '';
    width: 100%;
    height: 100%;
    background: url('~@/assets/bg.jpg') 0 0 no-repeat;
    background-size: cover;
    position: absolute;
    filter: blur(3px);
    transform: scale(1.01);
    overflow: hidden;
  }

  .login {
    width: 100%;
    height: 100%;
  }

  .input {
    width: fit-content;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 2em;
    right: 0;
    margin: auto;
    height: 300px;
    color: white;
    font-family: 'Times New Roman', Times, serif;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .contact {
    width: fit-content;
    height: 2em;
    position: absolute;
    bottom: 1.5em;
    right: 1.5em;
    color: white;
    font-size: 0.8em;
  }

  .contact-show {
    font-size: 0.8em;
    color: white;
    background-color: transparent;
    border: 0;
  }
</style>