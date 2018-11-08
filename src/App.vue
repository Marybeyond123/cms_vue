<template>
  <div class="app">
   <!-- 左边 -->
    <div class="leftDiv">
    <!-- 左边头部 -->
    <div class="topLeft">
      <img src="./assets/images/logo.png" alt="" width="40" height="40" style="margin:0 20px">
      看点资讯
    </div>
    <div class="contentLeft">
      <ul>
          <li>
            <i class="iconfont icon-shouye"></i>
            <router-link to='/'>首页</router-link>
            <i class="iconfont icon-kuozhan"></i>
          </li>
          <li>
            <i class="iconfont icon-liebiao"></i>
            <router-link to="/category">栏目管理</router-link>
            <i class="iconfont icon-kuozhan"></i>
          </li>
          <li>
            <i class="iconfont icon-zixun"></i>
            <router-link to='/article'>咨询管理</router-link>
            <i class="iconfont icon-kuozhan"></i>
          </li>
          <li>
            <i class="iconfont icon-ai-user"></i>
            <router-link to='/user'>用户管理</router-link>
            <i class="iconfont icon-kuozhan"></i>
          </li>
          <li>
            <i class="fa fa-cog"></i>
            <router-link to='/setting'>系统设置</router-link>
            <i class="fa fa-angle-right"></i>
          </li>
      </ul>
    </div>
  </div>
  <!-- 右边 -->
  <div class="rightDiv">
    <!-- 右边头部 -->
    <div class="topRight">
      <div class="noticeDiv">
        <i class="iconfont icon-liebiao1"></i>
        <i class="iconfont icon-laba"></i>
        <span class="noticeNum">4</span>
      </div>
      <div class="infoDiv">
          <img class="photo" :src="user.userface" alt="">
        <div class="u">
         <el-dropdown @command='handleCommand'>
            <span class="el-dropdown-link">
              {{user.nickname}} <i class="el-icon-arrow-down el-icon--right"></i>
            </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>个人中心</el-dropdown-item>
            <el-dropdown-item command='logout'>退出</el-dropdown-item>
          </el-dropdown-menu>
         </el-dropdown>
        </div>
      </div>
    </div>
    <!-- 右边内容 -->
    <div class="contentRight">
        <div class="wrapper">
          <router-view></router-view>
        </div>
    </div>
  </div>
  </div>
</template>
<script>
  import axios from '@/http/axios'
 //引入iconfont
import './assets/iconFont/iconfont.css'
  export default {
     data(){
      return {
        currentRoute:'/',
        user:{}
      }
    },
    watch:{
      '$route':function(to,from){
        this.currentRoute = to.path;
      }
    },
    created(){
      this.currentRoute = this.$route.path;
      // 从localStorage中获取用户信息，用于在页面中显示
      
      let user = JSON.parse(localStorage.getItem('user'));
      if(user && user.id){
        this.user = user;
      } else {
        window.vm.currentComponent = 'Login';
      }
      
    },
    methods:{
      handleCommand(command){
        if(command == 'logout'){
          axios.get('/logout').then(()=>{
            //跳转
            window.vm.currentComponent = 'Login';
            //清理localstorage中的user
            localStorage.removeItem('user');
          });
        }
      }
    }



  }
</script>
<style>
html {
    font: normal normal 12px '微软雅黑','Microsoft YaHei';
    color: #666
  }
  body , ul ,ol,dl ,p, h1,h2,h3 {
    margin: 0;
    padding: 0
  }
  ul , ol {
    list-style: none;
  }
  a {
    color: #666;
    text-decoration: none;
  }
  div {
    box-sizing: border-box;
  }
.leftDiv{
  width: 17%;
  height:630px;
  background: #282830;
  color:white;
  display: inline-block;
}
.topLeft{
  height: 50px;
  line-height: 50px;
  background: #3D556D;
  font-size: 20px;
  font-family: "微软雅黑";
}
.contentLeft{
  padding-top:20px;
}
.contentLeft li{
  padding:10px 0;
  line-height: 30px;
  font-size:18px;
  border-bottom:2px solid #333333;
  cursor: pointer;
}
.contentLeft i:first-child{
  margin-left:20px;
  margin-right:10px;
  font-size:20px;
}
.contentLeft i:last-child{
  float:right;
  margin-right:20px;
  font-size:20px;
}
.contentLeft > ul > li.current {
    background-color: #f0f0f0;
  }
/*右侧*/
.rightDiv{
  width: 83%;
  float: right;
}
.rightDiv .topRight{
  height: 50px;
  line-height: 50px;
  position: relative; 
}
/*右侧上部信息*/
.topRight i{
  font-size:30px;
  margin:0 20px;
}
.noticeDiv{
  display: inline-block;
  height: 50px;
}
.topRight .noticeNum{
  background-color: red;
  border-radius: 50%;
  display: inline-block;
  height: 18px;
  width: 18px;
  position: absolute;
  top:10px;
  left:115px;
  line-height: 18px;
  text-align: center;
  color: white;
  font-weight: 900;
}
.topRight .infoDiv{
  float: right;
  height: 50px;
}
.rightDiv .infoDiv img{
  width: 40px;
  height: 40px;
  border-radius:50%;
   margin-top: 5px;
    margin-right: 1em;
}
.infoDiv .u{
    float: right;
    line-height:50px;
    /*margin-top: 20px;*/
}
.topRight .infoDiv .el-dropdown{
    color:#666666;
  }

.contentRight{
  background: #F0F0F0;
  width: 100%;
  height:580px;
  padding:10px;
  overflow-y:auto;
}
.contentRight>.wrapper{
  /*overflow-y: outo;*/

}
</style>