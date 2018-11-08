<template>
	<div class="login">
		<div class="header">
		  <div class="title"><i class="fa fa-tv"></i>看点咨询管理系统</div>
		</div>		
		<!-- {{form}} -->
		    <div class="wrap">
	        <div class="logGet">
			<!-- 头部提示信息 -->
			<div class="logD logDtip">
				<p class="p1">登录</p>
			</div>
			<!-- 输入框 -->
			<div class="lgD">
				<el-form ref='userForm' :rules="rules" :model="form" label-position='left' size='small'>
			    <el-form-item prop='username' label="用户名" label-width="80px">
			      <el-input v-model="form.username" ></el-input>
			    </el-form-item>
			    <el-form-item prop='password' label="密码" label-width="80px">
			      <el-input v-model="form.password" type="password"></el-input>
			    </el-form-item>
			  </el-form>
			</div>
			<div class="bt">
				<el-button @click='login' size='small'>登录</el-button>
			</div>
		</div>
      </div>
      <div class="footer">
		  <div class="copyright">
		    <p>Copyright © 2018 Qunar.com Inc. All Rights Reserved.</p>
		    <div class="img">
				<i class="fa fa-envelope-o"></i><span>联系邮箱：zhangsan@qq.com</span>
			</div>
			
			<div class="img">
				<i class="fa fa-address-book-o"></i><span>联系地址：兰州市安宁区</span>
			</div>
			  
			<div class="img">
			  <i class="fa fa-volume-control-phone"></i><span>联系电话：121123</span>
			</div>
		 
 
  </div>
	
</div>

			
			

	</div>
</template>
<script>
	import axios from '@/http/axios'
	export default {
		data(){
			return {
				form:{

				},
				rules:{
					username:[{
						required:true,
						message:'请输入用户名',
						trigger:'blur'
					}],
					password:[{
						required:true,
						message:'请输入密码',
						trigger:'blur'
					}]
				}
			}
		},
		methods:{
			login(){
				//在登陆前校验
				this.$refs.userForm.validate((valid)=>{
					if(valid){
						axios.post('/login',this.form)
					.then(({data:result})=>{
						console.log(result);
						if(result.status == 200 && result.message =='登录成功'){
							//1.跳转到后台管理页面
							window.vm.currentComponent = 'App';
							//2.将登陆成功的用户信息保存到浏览器中

							localStorage.setItem('user',JSON.stringify(result.data));
						}
						// this.$root.currentComponent = 'App';
					})
					.catch((error)=>{
						console.log('error',error);
					});
					}
				});



			}
		}
	}
</script>

<style>
*{
	margin: 0;
	padding: 0;
}
.login{
	height: 600px;
}
.wrap{
	height: 500px;
	background-color: #3d556d; 
}
.header {
	height: 60px;
	width: 100%;
	background-color: #3d556d;
	color:#fff;
	font-size: 28px;
	position: relative;
}
.header .title{
	line-height: 60px;
	text-align: center;	
	padding-top: .2em;
}
.header .title i{
	margin-right: .5em;
}
.wrap .logGet {
	height: 300px;
	width: 350px;  
	position: absolute;
	background-color: #FFFFFF;
	top: 150px;
	right: 100px;
}
.logGet .logD.logDtip .p1 {
	display: inline-block;
	font-size: 28px;
	margin-top: 30px;
	width: 90%;
}
.wrap .logGet .logD.logDtip {
	width: 95%;
	border-bottom: 1px solid #f0f0f0;
	margin-bottom: 50px;
	margin-top: 0px;
	margin-right: auto;
	margin-left: auto;
}
.bt{
	float: right;
}
.footer{
	width: 100%;
	height: 100px;
	font-size: 12px;
	line-height:1.5em;
	text-align: center;
	background-color: #282830;
	position: absolute;
	color: #fff;
	bottom: 0;
	top:550px;
	right: 0;
}
.copyright{
	margin-top:2em;
}
.img i{
	margin-right: 1em;
}
</style>