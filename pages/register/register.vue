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
					<input type="text" class="login-form-input" placeholder="手机号码"/>
				</view>
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.password"></image>
					<input type="text" class="login-form-input"  placeholder="登录密码" password/>
				</view>
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.password"></image>
					<input type="text" class="login-form-input"  placeholder="确认密码" password/>
				</view>
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.cert"></image>
					<input type="text" class="login-form-input"  placeholder="验证码" style="width:420upx;"/>
					<text style="width:180upx;text-align: right;color:#DA53A2;font-size: 28upx;">获取验证码</text>
				</view>
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.code"></image>
					<input type="text" class="login-form-input"  placeholder="邀请码" />
				</view>
				<view style="padding-top:90upx;">
					<fun-button value="注 册" large></fun-button>
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
				imageLib:{
					logo:'../../static/bg/logo.png',
					phone:'../../static/icons/icon_shoujihao.png',
					password:'../../static/icons/icon_mima.png',
					cert:'../../static/icons/icon_yanzhengma.png',
					code:'../../static/icons/icon_yaoqingma.png',
				}
			};
		},
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
