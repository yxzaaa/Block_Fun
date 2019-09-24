<template>
	<view class="container">
		<uni-background src="../../static/bg1.jpg"/>
		<uni-nav-bar title="我要还款" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<div class="app-container full fixbutton">
			<view class="modal-box" v-if="showPwdModal">
				<view class="modal">
					<view class="modal-top-item">
						<view class="modal-title">请输入您的支付密码</view>
						<view class="modal-content">
							<password-inputer @input="setPassword" :value="password"></password-inputer>
						</view>
						<view style="font-size: 24upx;color: #1F1A1A;padding:40upx 40upx 20upx;text-align: center;">确定抵押后，您抵押的 Forest 将自动冻结</view>
					</view>
					<view class="modal-btns">
						<view @click="showPwdModal = false">取消</view>
						<view style="border-left:1px solid #eee;color:#0A61C9;" @click="publish">确定</view>
					</view>
				</view>
			</view>
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button 
						value="确定还款" 
						width="670upx"  
						large 
						@handle="putPassword"
					></fun-button>
				</view>
			</view>
			<view class="user-info" style="padding-top:40upx;">
				<text style="font-size: 26upx;">待还金额</text>
			</view>
			<view class="user-count">
				<text style="font-family: 'Montserrat-Bold';font-size:64upx;">1200</text>
				<text>USDT</text>
			</view>
			<view class="user-info">
				<text style="color:rgba(255,255,255,0.5);font-size: 26upx;">最后还款日:
					<span>2019/03/30</span>
				</text>
			</view>
			<view style="padding:40upx;">
				<view class="fun-card">
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">借款金额（USDT）</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">2000</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">抵押数量（Forest）</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">800</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">日利率</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">0.1%</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">综合利率</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">1.5%</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">手续费（USDT）</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">5</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">总利息（USDT）</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">20 USDT</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">周期</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">15月</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">借款日</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">2019/03/12</text>
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
				erweima:'../../static/image.png',
				userInfo:{
					avatar:'../../static/avatar/fortoken.png',
					username:'Xdog',
					usercount:'+8089.23'
				},
				showPwdModal:false,
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			putPassword(){
				if(this.showPwdModal){
					this.showPwdModal = false;
				}else{
					this.showPwdModal = true;
				}
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
				color:#fff;
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
