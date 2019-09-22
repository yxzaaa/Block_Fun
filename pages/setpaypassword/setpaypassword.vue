<template>
	<view class="container">
		<uni-background src="../../static/bg/login_bg.jpg"/>
		<uni-nav-bar title="创建钱包" textColor="#fff" layout="center"></uni-nav-bar>
		<view class="app-container full" style="padding-left:40upx;padding-right:40upx;">
			<view class="fun-card">
				<view class="fun-card-item notify">
					<image src="../../static/icons/icon_tishiicon.png"></image>
					<view>
						系统检测到您是首次登录，请设置您的钱包密码系统将会为您创建一个新的钱包账户。
					</view>
				</view>
			</view>
			<view class="fun-card">
				<view class="fun-card-item notify">
					<image src="../../static/icons/icon_tishiicon.png"></image>
					<view>
						为了您的账户安全，系统不会储存您的账户密码。因此钱包密码一旦设置后不可更改，不可找回。【请务必牢记您的钱包密码】
					</view>
				</view>
			</view>
			<view class="fun-card" v-if="needCode">
				<view class="fun-card-item notify" style="display: block;">
					<input v-model="checkCode" type="number" maxlength="6" placeholder="请输入验证码" style="width:100%;text-align:center;line-height: 64upx;font-size: 28upx;height:64upx;color:#fff;margin-bottom:30upx;">
					<fun-button :value="codeDelay == 0?'获取验证码':codeDelay+' s'" width="240upx" style="margin:auto;" @handle="getCode()"></fun-button>
				</view>
			</view>
			<view style="margin-top:120upx;">
				<fun-button value="设置密码" large block @handle="showModal = true;"></fun-button>
			</view>
			<view class="modal-box" v-if="showModal">
				<view class="modal">
					<view class="modal-top-item">
						<view class="modal-title">设置您的支付密码</view>
						<view class="modal-content">
							<password-inputer @input="setPassword" :value="initPassword"></password-inputer>
						</view>
					</view>
					<view class="modal-btns">
						<view @click="showModal = false">取消</view>
						<view style="border-left:1px solid #eee;color:#0A61C9;" @click="init">设置</view>
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
	import PasswordInputer from '@/components/possword-inputer.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			FunButton,
			PasswordInputer
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
				password:'',
				checkCode:'',
				initPassword:'',
				needCode:false,
				codeDelay:0,
				codeTimer:null,
				showModal:false,
				payToken:'',
				phone:'',
				auth:'',
			};
		},
		onLoad(option){
			if(option.token){
				//使用pay_token设置交易密码
				this.payToken = option.token;
				this.phone = option.mobile;
				this.password = option.password;
			}else if(option.auth){
				//使用验证码设置交易密码
				this.needCode = true;
				this.phone = option.mobile;
				this.auth = option.auth;
			}
		},
		methods:{
			setPassword(val){
				this.initPassword = val;
			},
			//获取验证码
			getCode(){
				if(this.codeDelay === 0 && this.phone.length === 13){
					this.$http({
						url:'/v1/users/login/forget-login-password/send-code?login_name='+this.phone,
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
				}
			},
			init(){
				if(this.initPassword.length === 8){
					if(this.needCode){
						//使用验证码进行初始化支付密码
						this.$http({
							url:'/v1/main/users/reset-confirm-account-payment-password',
							header:{
								"Content-Type":"application/json",
								"Authorization":this.auth,
							},
							data:{
								validate_code:this.checkCode,
								pay_password:this.initPassword,
								pay_password_hash:this.$md5(this.initPassword)
							},
							success:res=>{
								console.log(res);
								if(res.code == 200){
									uni.showToast({
										title:'支付密码设置成功，请牢记！',
										icon:'none'
									})
									setTimeout(()=>{
										//延时1s后获取用户信息，放在本地存储中
										this.$http({
											url:'/v1/main/users/user-info',
											header:{
												"Content-Type":"application/json",
												"Authorization":this.auth,
											},
											success:res=>{
												if(res.code == 200){
													uni.setStorage({
														key: 'userInfo',
														data:res.data,
														success:res=>{
															uni.switchTab({
																url:'../index/index'
															})
														}
													})
												}else{
													uni.navigateTo({
														url:'../login/login'
													})
												}
											}
										})
									},1000)
								}else{
									uni.showToast({
										title:res.message,
										icon:'none'
									})
								}
							}
						})
					}else{
						//使用pay_token发送设置支付密码请求
						this.$http({
							url:'/v1/users/register/set-pay',
							data:{
								pay_token:this.payToken,
								pay_password:this.initPassword,
								pay_password_hash:this.$md5(this.initPassword)
							},
							success:res=>{
								console.log(res);
								if(res.code == 200){
									//设置成功后给出提示
									uni.showToast({
										title:'支付密码设置成功，请牢记！',
										icon:'none'
									})
									setTimeout(()=>{
										//进行登录操作
										this.$http({
											url:'/v1/users/login',
											data:{
												login_name:this.phone,
												password:this.password,
												password_hash:this.$md5(this.password)
											},
											success:res=>{
												console.log(res);
												if(res.code == 200){
													uni.setStorage({
														key: 'userInfo',
														data:res.data,
														success:res=>{
															uni.switchTab({
																url:'../index/index'
															})
														}
													})
												}else{
													uni.navigateTo({
														url:'../login/login'
													})
												}
											}
										})
									},1000)
								}else{
									uni.showToast({
										title:res.message,
										icon:'none'
									})
								}
							}
						})
					}
				}else{
					uni.showToast({
						title:'请输入8位支付密码',
						icon:'none'
					})
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.fun-card{
		margin-top:30upx;
	}
	.notify{
		width:100%;
		display: flex;
		justify-content: space-between;
		image{
			width:36upx;
			height:36upx;
			margin-top:4upx;
		}
		view{
			width:calc(100% - 56upx);
			color:#fff;
			font-size: 26upx;
			line-height: 48upx;
		}
	}
</style>
