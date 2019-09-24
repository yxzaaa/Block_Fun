<template>
	<view class="container">
		<uni-background src="../../static/bg/login_bg.jpg"/>
		<uni-nav-bar title="用户注册" textColor="#fff" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="logo-box">
				<image :src="imageLib.logo"></image>
				<view>X-wallet</view>
			</view>
			<view class="login-form">
				<view class="login-form-item" style="display: flex;justify-content: space-between;">
					<view style="display: flex;justify-content: flex-start;">
						<image class="login-form-label" :src="imageLib.phone"></image>
						<input type="number" class="login-form-input" style="width:420upx;" placeholder="手机号码" v-model="phone"/>
					</view>
					<picker @change="countryChange" :value="currCountry" :range="countryLib" mode="selector">
						<view 
						style="padding:0upx 20upx;border-radius: 6upx;background: #2D1F25;line-height: 48upx;color:#fff;display: flex;justify-content: center;align-items: center;margin-right:20upx;">
							<text style="#999;font-size: 24upx;">{{countryLib[currCountry]}}</text>
							<image :src="imageLib.sanjiao" style="width:20upx;height:14upx;margin-left:6upx;"></image>
						</view>
					</picker>
				</view>
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.password"></image>
					<input type="password" class="login-form-input" style="width:420upx;"  placeholder="登录密码" password v-model="password"/>
				</view>
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.password"></image>
					<input type="password" class="login-form-input" style="width:420upx;" placeholder="确认密码" password v-model="confirmPassword"/>
				</view>
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.cert"></image>
					<input type="number" class="login-form-input"  placeholder="验证码" style="width:420upx;" v-model="checkCode"/>
					<text style="width:180upx;text-align: center;color:#DA53A2;font-size: 26upx;" @click="getCode">
						{{codeDelay === 0?'获取验证码':codeDelay+' s'}}
					</text>
				</view>
				<view class="login-form-item" style="display: flex;justify-content: space-between;">
					<view style="display: flex;justify-content: flex-start;">
						<image class="login-form-label" :src="imageLib.code"></image>
						<input type="text" class="login-form-input" style="width:420upx;" placeholder="邀请码" v-model="visitCode"/>
					</view>
					<text style="width:100upx;text-align: center;color:#999;font-size: 26upx;">
						选填
					</text>
				</view>
				<view style="padding-top:90upx;">
					<fun-button value="注 册" large @handle="register"></fun-button>
				</view>
				<view class="horizon-list" style="text-align:center;font-size: 24upx;color:#DA53A2;">
					<text>点击注册表示您同意《用户注册协议》</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import FunButton from '@/components/fun-button.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			FunButton
		},
		data() {
			return {
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					}
				},
				imageLib:{
					logo:'../../static/bg/logo.png',
					sanjiao:'../../static/icons/sanjiao.png',
					phone:'../../static/icons/icon_shoujihao.png',
					password:'../../static/icons/icon_mima.png',
					cert:'../../static/icons/icon_yanzhengma.png',
					code:'../../static/icons/icon_yaoqingma.png',
				},
				phone:'',
				password:'',
				confirmPassword:'',
				registerSid:'',
				checkCode:'',
				visitCode:'',
				codeDelay:0,
				codeTimer:null,
				currCountry:0,
				countryLib:[
					'中国','美国','欧洲','日本'
				]
			};
		},
		methods:{
			countryChange(e){
				this.currCountry = e.target.value;
			},
			getCode(){
				if(this.codeDelay === 0 && this.phone.length === 11){
					this.$http({
						url:'/v1/users/register/send-code?login_name='+'86'+this.phone,
						success:res=>{
							console.log(res);
							if(res.code == 200){
								// this.registerSid = res.result.sid;
								this.codeDelay = 60;
								this.codeTimer = setInterval(()=>{
									if(this.codeDelay>0){
										this.codeDelay --;
									}else{
										clearInterval(this.codeTimer);
										this.codeTimer = null;
									}
								},1000);
							}else{
								uni.showToast({
									title:res.message,
									icon:'none'
								})
							}
						}
					})
				}else if(this.phone.length !== 11){
					uni.showToast({
						title:"请输入正确的手机号码",
						icon:'none'
					})
				}
			},
			register(){
				if(this.password === this.confirmPassword){
					this.$http({
						url:'/v1/users/register',
						data:{
							login_name:'86'+this.phone,
							password:this.password,
							password_hash:this.$md5(this.password),
							invite_code:this.visitCode,
							validate_code:this.checkCode
						},
						success:res=>{
							console.log(res);
							if(res.code == 200){
								//注册成功后,跳转设置交易密码页面,带pay_token，phone,password
								uni.navigateTo({
									url:'../setpaypassword/setpaypassword?token='+res.data.pay_token+'&mobile=86'+this.phone+'&password='+this.password
								})
							}else{
								uni.showToast({
									title:res.message,
									icon:'none'
								})
							}
						}
					})
				}else{
					uni.showToast({
						title:"两次输入的密码不一致",
						icon:'none'
					})
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.logo-box{
		width:750upx;
		display: flex;
		justify-content: center;
		align-items: center;
		flex-wrap:wrap;
		padding:40upx;
		image{
			width:120upx;
			height:120upx;
		}
		view{
			width:100%;
			text-align: center;
			font-size: 28upx;
			font-weight: bold;
			color:#fff;
			padding:20upx;
		}
	}
	.login-form{
		width:750upx;
		padding:0px 60upx;
		.login-form-item{
			width:630upx;
			border-bottom:1px solid rgba(255,255,255,0.1);
			padding-top:45upx;
			padding-bottom:20upx;
			display:flex;
			justify-content:flex-start;
			align-items:center;
			.login-form-label{
				width:32upx;
				height:32upx;
			}
			.login-form-input{
				width:600upx;
				color:#fff;
				padding-left:40upx;
				font-size:28upx;
				line-height: 36upx;
			}
		}
	}
	.horizon-list{
		padding:40upx 0upx;
		.horizon-list-item{
			display: flex;
			justify-content: space-between;
			align-items: center;
			.left-item{
				width:400upx;
				.left-item-title{
					display: block;
					color:#fff;
					font-size: 32upx;
					line-height: 52upx;
					font-family:'Montserrat-Bold';
					span{
						font-family:'Montserrat-Bold';
					}
				}
				.left-item-date{
					display: block;
					color:#999;
					font-size: 26upx;
					line-height: 52upx;
				}
			}
			.right-item{
				width:300upx;
				display: flex;
				justify-content: flex-end;
				align-items: center;
				.right-item-text{
					display: block;
					color:#999;
					font-size: 26upx;
					line-height: 52upx;
				}
				image{
					width:42upx;
					height:42upx;
					margin-left:10upx;
				}
			}
		}
	}
</style>
