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
			<fun-button value="设置密码" large block style="margin-top:120upx;" @handle="showModal = true;"></fun-button>
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
				showModal:false,
				payToken:''
			};
		},
		onLoad(option){
			if(option.token){
				//使用pay_token设置交易密码
				this.payToken = option.token;
			}else{
				//使用验证码设置交易密码
				this.needCode = true;
			}
		},
		methods:{
			setPassword(val){
				this.initPassword = val;
			},
			init(){
				console.log(this.initPassword);
				if(this.initPassword.length ==6){
					if(this.needCode){
						
					}else{
						//使用pay_token发送设置支付密码请求
						this.$http({
							url:''
						})
					}
				}else{
					uni.showToast({
						title:'请输入六位支付密码',
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
