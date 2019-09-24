<template>
	<view class="container">
		<uni-background src="../../static/bg1.jpg"/>
		<uni-nav-bar :title="infos.type==1?'我要借款':'我要投资'" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<div class="app-container full fixbutton">
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
						<view style="border-left:1px solid #eee;color:#0A61C9;" @click="acceptBill">{{infos.type == 1?'抵押':'投资'}}</view>
					</view>
				</view>
			</view>
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button 
						:value="infos.type == 1?'确定抵押':'确认投资'" 
						width="670upx"  
						large 
						@handle="showPwdModal = true"
					></fun-button>
				</view>
			</view>
			<view class="user-info" style="padding-top:40upx;">
				<text>总利息</text>
			</view>
			<view class="user-count">
				<text style="font-family: 'Montserrat-Bold';font-size:64upx;">{{getNum(infos.income)}}</text>
				<text>USDT</text>
			</view>
			<view class="user-info">
				<text style="color:rgba(255,255,255,0.5);font-size: 26upx;">月利率{{infos.rate*100}}%</text>
			</view>
			<view style="padding:40upx;">
				<view class="fun-card">
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">Forest 单价</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">{{getNum(infos.price)}} USDT/{{infos.unit}}</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">投资总量</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">{{getNum(infos.total)}} USDT</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">投资周期</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">{{infos.month}} 月</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">抵押总量</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">{{infos.amount}}</text>
							</view>
						</view>
						<!-- <view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">我要借款</text>
							</view>
							<view class="right-item">
								<input style="font-size: 26upx;color:#fff;text-align: right;" type="text" placeholder="请输入您的借款金额"/>
							</view>
						</view> -->
						<view style="width:100%;height:3upx;background:rgba(255,255,255,0.2);margin:20upx 0upx;"></view>
						<!-- <view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">需要抵押</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">15 个</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">还款方式</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">先息后本</text>
							</view>
						</view> -->
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">手续费</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">{{infos.fee}} USDT</text>
							</view>
						</view>
					</view>
				</view>
			</view>
		</div>
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
				infos:{},
				password:'',
				showPwdModal:false
			};
		},
		onLoad(){
			//获取挂单信息
			uni.getStorage({
				key:'accept_bill_info',
				success:res=>{
					this.infos = res.data;
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
			acceptBill(){
				//接受此挂单
				this.$http({
					url:'/v1/main/debit/debit-order-request',
					data:{
						id:this.infos.id,
						coin:this.infos.unit,
						password:this.password
					},
					success:res=>{
						if(res.code == 200){
							uni.showToast({
								title:this.infos.type == 1?'抵押成功':'投资成功',
								icon:'none'
							})
							setTimeout(()=>{
								uni.navigateBack({
									delta:1
								})
							},1500)
						}
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.user-info{
		width:750upx;
		display:flex;
		justify-content:center;
		align-items:center;
		padding:10upx 0;
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
		padding:10upx 0;
		text{
			color:#fff;
			font-size: 44upx;
			padding:0px 10upx;
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
	.horizon-list-item{
		padding:16upx 0upx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		.left-item{
			display:flex;
			justify-content:flex-start;
			align-items:center;
			.left-item-avatar{
				width:40upx;
				height:40upx;
				margin-right:20upx;
			}
			.left-item-name{
				color:#fff;
				font-size: 26upx;
				padding-right:15upx;
			}
			.left-item-label{
				color:#999;
				font-size: 24upx;
				margin-right: 18upx;
			}
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
				font-family:'Montserrat-Light';
			}
		}
		.right-item{
			display:flex;
			justify-content:flex-end;
			align-items:center;
			color:#999;
			font-size: 24upx;
			.left-item-name{
				color:#fff;
				font-size: 26upx;
			}
			.right-item-text{
				font-size: 38upx;
				color:#56CCF2;
				font-family:'Montserrat-Bold';
				span{
					font-family:'Montserrat-Bold';
				}
			}
			image{
				width:42upx;
				height:42upx;
				margin-left:10upx;
			}
		}
	}
</style>
