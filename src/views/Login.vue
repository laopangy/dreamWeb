<template>
  <div class="login" id="login" :style="{backgroundImage:`url(${loginBackgroundImg})`}">
    <el-container style="height: 100%">
      <el-header style="text-align: right; font-size: 20px">
        <el-dropdown>
          <i class="el-icon-setting" style="font-size: 25px; margin-top: 15px;color: #42b983"></i>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item @click.native="setBackgroundImg()">切换主题</el-dropdown-item>
            <el-dropdown-item>待补充</el-dropdown-item>
            <el-dropdown-item>待补充</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-header>

      <el-form :rules="rules" ref="loginForm" :model="loginForm" class="loginContainer">
        <h3 class="loginTitle">Dream登录</h3>
        <el-form-item prop="userName">
          <el-input type="text" v-model="loginForm.userName" auto-complete="off" placeholder="请输入用户名"></el-input>
        </el-form-item>
        <el-form-item prop="passWord">
          <el-input type="text" v-model="loginForm.passWord" auto-complete="off" placeholder="请输入密码" @keydown.enter.native="submitLogin" show-password></el-input>
        </el-form-item>
        <el-button type="primary" style="width:100%;" @click="submitLogin">登录</el-button>
      </el-form>
    </el-container>
  </div>
</template>



<script>
import backgroundImg1 from "../assets/images/background/c586cac74b474b5ea5458a046e8b14c0.jpg";
import backgroundImg2 from "../assets/images/background/c9d3deb2880411ebb6edd017c2d2eca2.jpg";
import backgroundImg3 from "../assets/images/background/c8bfcd9f880411ebb6edd017c2d2eca2.jpg";
import backgroundImg4 from "../assets/images/background/wallhaven-qzmzvd_1920x1080.png";
import {postRequest} from "@/utils/api";
// import postKeyValueRequest from "../utils/api";
export default {
  name: 'Login',
  data() {
    return {
      loginForm: {
        userName: 'pangy',
        passWord: '123'
      },
      checked: true,
      rules: {
        userName: [{required: true, message: '请输入用户名', trigger: 'blur'}],
        passWord: [{required: true, message: '请输入密码', trigger: 'blur'}]
      },
      imgIndex : 0,
      loginBackgroundImg: backgroundImg1,
      imgList:[{"id":0,"url":backgroundImg1},{"id":1,"url":backgroundImg2},{"id":2,"url":backgroundImg3},{"id":3,"url":backgroundImg4}]
    }
  },methods:{
    //复制背景图
     setBackgroundImg(){
       this.imgIndex = this.imgIndex+1;
        if (this.imgIndex>this.imgList.length-1){
          this.imgIndex = 0;
        }
        this.loginBackgroundImg = this.imgList[this.imgIndex].url;
       console.log(this.imgIndex);
     },
    submitLogin() {
      this.$refs.loginForm.validate((valid) => {
        if (valid) {
          this.postRequest("/user/getByLogin",this.loginForm).then(resp =>{
            if (resp.data){
              let path = this.$route.query.redirect;
              this.$router.replace(path=='/'||path==undefined?'/home':path);
            }else{
              this.$message.error('账号或者密码输入错误，请重新输入！！！');
              return false;
            }
          })
        } else {
          this.$message.error('请输入所有字段')
          return false;
        }
      });
    }
  }
}
</script>

<style>
#login{
  position : absolute;
  width : 100%;
  height : 100%;
  /* 加载背景图 */
  //background-image: url("../assets/images/background/c586cac74b474b5ea5458a046e8b14c0.jpg");
  /* 背景图垂直、水平均居中 */
  background-position: center center;
  /* 背景图不平铺 */
  background-repeat: no-repeat;
  /* 当内容高度大于图片高度时，背景图像的位置相对于viewport固定 */
  background-attachment: fixed;
  /* 让背景图基于容器大小伸缩 */
  background-size: cover;
  /* 设置背景颜色，背景图加载过程中会显示背景色 */
  //background-color: #464646;
}
.loginContainer{
  border-radius: 15px;
  background-clip: padding-box;
  margin: 180px auto;
  width: 350px;
  padding: 15px 35px 15px 35px;
  background: rgba(0, 0, 0, .2);
  border: 1px solid #eaeaea;
  box-shadow: 0 0 25px #cac6c6;
}
.loginTitle {
  margin: 15px auto 20px auto;
  text-align: center;
  color: #42b983;
}
body {
  margin: 0;
  padding: 0;
}
</style>