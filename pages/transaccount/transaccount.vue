<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="转账" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="modal-box" v-if="showPwdModal">
				<view class="modal">
					<view class="modal-top-item">
						<view class="modal-title">请输入您的交易密码</view>
						<view class="modal-content">
							<password-inputer @input="setPassword" :value="password"></password-inputer>
						</view>
					</view>
					<view class="modal-btns">
						<view @click="showPwdModal = false">取消</view>
						<view style="border-left:1px solid #eee;color:#0A61C9;" @click="submitTrans">转账</view>
					</view>
				</view>
			</view>
			<view class="status-box" style="padding:20upx 40upx;">
				<view class="left-status">
					<image :src="imageLib.logosmall" style="width:40upx;height:40upx;" />
					<text style="font-size:30upx;font-family:'Montserrat-Light';color:#fff;">Forbidden {{coin}} Coin</text>
					<text style="font-size:26upx;color:#999;">{{coin}}</text>
				</view>
			</view>
			<view class="fun-card" style="margin:30upx 40upx;width:670upx;">
				<view class="fun-card-item">
					<view class="form-item">
						<view class="form-label">接收地址</view>
						<view class="form-value-box">
							<view class="form-input-box">
								<input v-model="toAddr" class="form-input-field" placeholder="输入地址"/>
								<view class="form-input-btns">
									<image @click="scanCode" :src="imageLib.scan" />
									<image :src="imageLib.contacts" />
								</view>
							</view>
						</view>
					</view>
					<view class="form-item">
						<view class="form-label">转账金额</view>
						<view class="form-value-box">
							<view class="form-input-box">
								<input v-model="amount" class="form-input-field" :placeholder="'可用余额 '+total+' '+coin"/>
								<view class="form-input-btns">
									<text @click="amount = total">转出全部</text>
								</view>
							</view>
						</view>
						<view style="font-size: 24upx;color:#999;padding-bottom:30upx;">最低转出 {{minCount}} 个</view>
					</view>
					<view class="form-item">
						<view class="form-label" style="margin-bottom:20upx;">添加备注</view>
						<view class="input-field" style="padding:20upx 30upx;">
							<input v-model="remark" style="width:100%;font-size: 26upx;color:#c7c7c7;" placeholder="点击添加"/>
						</view>
					</view>
					<view class="status-box handler-status">
						<view class="left-status">
							<text style="font-size:28upx;color:#fff;">手续费</text>
						</view>
						<view class="right-status">
							<text style="color:#fff;font-size: 26upx;font-family:'Montserrat-Light';">{{handlePay}}Xdog</text>
							<text style="display: inline-block;font-size:26upx;padding:0upx 20upx;color:#999;font-family:'Montserrat-Light';">|</text>
							<text style="font-size: 26upx;color:#999;font-family:'Montserrat-Light';">0.3%</text>
						</view>
					</view>
				</view>
				<view class="submit-btn" @click="showPwdModal = true">
					转账
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
				scroll:0,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					}
				},
				imageLib:{
					logosmall:'../../static/icons/logo_small.png',
					contacts:'../../static/icons/icon_contacts.png',
					scan:'../../static/icons/icon_scan.png'
				},
				erweima:'../../static/image.png',
				coin:'USDT',//币种
				total:'',
				handlePay:'',
				amount:'',
				toAddr:'',
				password:'',
				remark:'',
				minCount:0,
				showPwdModal:false,
			};
		},
		onLoad(option){
			console.log(option);
			//请求当前币种转账信息
			this.$http({
				url:'/v1/main/account/withdraw-preloading',
				data:{
					coin:option.coin
				},
				success:res=>{
					if(res.code == 200){
						this.coin = res.data.coin;
						this.total = res.data.amount;
						this.handlePay = res.data.rate;
						this.minCount = res.data.min_transfer_amount;
					}
				}
			})
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			setPassword(val){
				this.password = val;
			},
			getNum(num){
				return (parseFloat(num)).toFixed(2);
			},
			scanCode(){
				uni.scanCode({
					onlyFromCamera:true,
					success:res=>{
						this.toAddr = res.result;
					}
				})
			},
			//提交转账
			submitTrans(){
				this.$http({
					url:'/v1/main/account/withdraw-request',
					data:{
						coin: this.coin,
						amount: this.amount,
						to_address: this.toAddr,
						pay_password: this.password,
						remark: this.remark
					},
					success:res=>{
						if(res.code == 200){
							uni.showToast({
								title:'转账成功',
								icon:'none'
							})
							setTimeout(()=>{
								uni.navigateBack({
									delta:1
								})
							},1500)
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
	.handler-status{
		padding:30upx 0upx;
		.right-status{
			text{
				display: inline-block;
			}
		}
	}
	.user-info{
		width:750upx;
		display:flex;
		justify-content:center;
		align-items:center;
		padding:20upx 0;
		image{
			width:48upx;
			height:48upx;
			margin-right:20upx;
		}
		text{
			color:#fff;
			font-size: 32upx;
		}
	}
	.user-count{
		width:750upx;
		text-align:center;
		padding:30upx 0;
		text{
			color:#DA53A2;
			font-size: 52upx;
			font-family:'Montserrat-Bold';
		}
	}
	.erweima{
		width:200upx;
		height:200upx;
		background: #fff;
		border-radius: 12upx;
		margin:auto;
		padding:20upx;
		image{
			width:100%;
			height:100%;
		}
	}
</style>
