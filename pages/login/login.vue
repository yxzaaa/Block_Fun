<template>
	<view class="container">
		<uni-background src="../../static/bg/login_bg.jpg"/>
		<uni-nav-bar title="用户登录" textColor="#fff" layout="center"></uni-nav-bar>
		<view class="app-container full">
			<view class="logo-box">
				<image :src="imageLib.logo"></image>
				<view>X-wallet</view>
			</view>
			<view class="login-form">
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.phone"></image>
					<input type="number" class="login-form-input" placeholder="手机号码" maxlength="11" v-model="mobile"/>
				</view>
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.password"></image>
					<input type="password" class="login-form-input"  placeholder="登录密码" password maxlength="16" v-model="password"/>
				</view>
				<view style="padding-top:90upx;">
					<fun-button value="登 录" large @handle="login"></fun-button>
				</view>
				<view class="horizon-list">
					<view class="horizon-list-item">
						<view class="left-item">
							<navigator url="../passwordback/passwordback">
								<text class="left-item-date">忘记密码</text>
							</navigator>
						</view>
						<view class="right-item">
							<navigator url="../register/register">
								<text class="right-item-text">没有账号？去注册</text>
							</navigator>
						</view>
					</view>
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
				imageLib:{
					logo:'../../static/bg/logo.png',
					phone:'../../static/icons/icon_shoujihao.png',
					password:'../../static/icons/icon_mima.png',
					cert:'../../static/icons/icon_yanzhengma.png',
					code:'../../static/icons/icon_yaoqingma.png',
				},
				mobile:'',
				password:''
			};
		},
		onLoad(option){
			if(option.register === 'successs'){
				
			}
		},
		methods:{
			login(){
				this.$http({
					url:'/v1/users/login',
					data:{
						login_name:'86'+this.mobile,
						password:this.password,
						password_hash:this.$md5(this.password)
					},
					success:res=>{
						console.log(res);
						if(res.code == 200){
							if(res.data.payment_password_set == 0){
								//检查本地pay_token设置
								//跳转已登录状态设置交易密码
								uni.navigateTo({
									url:'../setpaypassword/setpaypassword?mobile=86'+this.mobile+'&auth='+res.data.token
								})
							}else{
								uni.setStorage({
									key: 'userInfo',
									data:res.data,
									success:res=>{
										uni.switchTab({
											url:'../index/index'
										})
									}
								})
							}
						}else{
							uni.showToast({
								title:res.message,
								icon:'none'
							})
						}
					}
				})
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
		padding:60upx;
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
