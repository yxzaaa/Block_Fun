<template>
	<view class="container">
		<uni-background src="../../static/bg/login_bg.jpg"/>
		<uni-nav-bar title="找回密码" textColor="#fff" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="logo-box">
				<image :src="imageLib.logo"></image>
				<view>X-wallet</view>
			</view>
			<view class="login-form">
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.phone"></image>
					<input type="number" class="login-form-input" placeholder="手机号码" maxlength="11" v-model="phone"/>
				</view>
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.cert"></image>
					<input type="number" class="login-form-input"  placeholder="验证码" style="width:420upx;" maxlength="6" v-model="checkCode"/>
					<text style="width:180upx;text-align: center;color:#DA53A2;font-size: 28upx;" @click="getCode">{{codeDelay === 0?'获取验证码':codeDelay+' s'}}</text>
				</view>
				<view class="login-form-item">
					<image class="login-form-label" :src="imageLib.password"></image>
					<input type="password" class="login-form-input"  placeholder="请输入8~16位新密码" password maxlength="16" v-model="password"/>
				</view>
				<view style="padding-top:90upx;">
					<fun-button value="确 认" large @handle="pwdBack"></fun-button>
				</view>
				<!-- <view style="padding-top:20upx;">
					<fun-button value="取消" type="text" color="#999" width="630upx"></fun-button>
				</view> -->
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
					phone:'../../static/icons/icon_shoujihao.png',
					password:'../../static/icons/icon_mima.png',
					cert:'../../static/icons/icon_yanzhengma.png',
					code:'../../static/icons/icon_yaoqingma.png',
				},
				codeDelay:0,
				codeTimer:null,
				phone:'',
				checkCode:'',
				password:'',
			};
		},
		methods:{
			getCode(){
				if(this.codeDelay === 0 && this.phone.length === 11){
					this.$http({
						url:'/v1/users/login/forget-login-password/send-code?login_name=86'+this.phone,
						success:res=>{
							console.log(res);
							if(res.code == 200){
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
			pwdBack(){
				this.$http({
					url:'/v1/users/login/forget-login-password/reset',
					data:{
						login_name:'86'+this.phone,
						new_password:this.password,
						new_password_hash:this.$md5(this.password),
						validate_code:this.checkCode
					},
					success:res=>{
						console.log(res)
						if(res.code == 200){
							uni.navigateTo({
								url:'../login/login?passwordback=success',
							})
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
