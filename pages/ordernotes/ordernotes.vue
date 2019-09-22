<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="订单记录" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="horizon-list-item" style="padding:20upx 40upx;">
				<view class="left-item" style="width:420upx;">
					<text class="left-item-name" style="color:rgba(255,255,255,0.5);">订单筛选</text>
				</view>
				<view class="right-item" style="height:48upx;">
					<picker @change="pickerChange" :value="currClass" :range="classLib" mode="selector">
						<view style="padding:0upx 20upx;height:100%;background: #2D1F25;line-height: 48upx;color:#fff;display: flex;justify-content: center;align-items: center;">
							<text style="color:#999;">{{classLib[currClass]}}</text>
							<image :src="imageLib.sanjiao" style="width:20upx;height:14upx;"></image>
						</view>
					</picker>
				</view>
			</view>
			<view class="translist">
				<block v-for="(item,index) in transList" :key="index">
					<navigator :url="'../walletorderdetail/walletorderdetail?orderid='+index">
						<view class="fun-card" style="margin-bottom: 40upx;">
							<view class="fun-card-item">
								<view class="horizon-list-item">
									<view class="left-item" style="width:500upx;">
										<image class="left-item-avatar" style="margin-right:5upx;" :src="item.sold?imageLib.sold:imageLib.bought"></image>
										<text class="left-item-name" :style="{color:item.sold?'#56CCF2':'#DA53A2'}">{{item.sold?'出售':'购买'}}</text>
										<text class="left-item-label">|</text>
										<text class="left-item-name">USDT</text>
									</view>
									<view class="right-item">
										<text class="left-item-name" style="color:#fff;">进行中</text>
									</view>
								</view>
							</view>
							<view class="fun-horizen"></view>
							<view class="fun-card-item">
								<view class="horizon-list-item">
									<view class="left-item">
										<text class="left-item-label">单号</text>
									</view>
									<view class="right-item">
										<text class="left-item-name">2AEF***PAFR</text>
									</view>
								</view>
								<view class="horizon-list-item">
									<view class="left-item">
										<text class="left-item-label">单价</text>
									</view>
									<view class="right-item">
										<text class="left-item-name">6.6868 CNY</text>
									</view>
								</view>
								<view class="horizon-list-item">
									<view class="left-item">
										<text class="left-item-label">数量</text>
									</view>
									<view class="right-item">
										<text class="left-item-name">100USDT</text>
									</view>
								</view>
								<view class="horizon-list-item">
									<view class="left-item">
										<text class="left-item-label">总金额</text>
									</view>
									<view class="right-item">
										<text class="left-item-name">669.68 CNY</text>
									</view>
								</view>
								<view class="horizon-list-item">
									<view class="left-item">
										<text class="left-item-label">卖家</text>
									</view>
									<view class="right-item">
										<text class="left-item-name">美好即将发生</text>
									</view>
								</view>
							</view>
						</view>
					</navigator>
				</block>
			</view>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import FunButton from '@/components/fun-button.vue';
	export default{
		components:{
			UniNavBar,
			UniBackground,
			FunButton
		},
		data(){
			return {
				scroll:0,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					}
				},
				imageLib:{
					sold:'../../static/icons/icon_sold.png',
					bought:'../../static/icons/icon_bought.png',
					alipay:'../../static/icons/icon_alipay.png',
					wechatpay:'../../static/icons/icon_wechatpay.png',
					unionpay:'../../static/icons/icon_unionpay.png',
					sanjiao:'../../static/icons/sanjiao.png'
				},
				transList:[
					{
						sold:false,
					},
					{
						sold:true,
					}
				],
				currClass:0,
				classLib:[
					'全部','进行中','仲裁中','已结束'
				]
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			pickerChange(e){
				this.currClass = e.target.value;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.fiexd-btn{
		position: fixed;
		right:70upx;
		bottom:120upx;
		background: #fff;
		width:98upx;
		height:96upx;
		border-radius: 48upx;
		box-shadow: 0px 0px 10px rgba(0, 9, 33, 0.4);
		display:flex;
		justify-content:center;
		align-items:center;
		z-index:998;
		image{
			width:64upx;
			height:64upx;
		}
	}
	.transout-tabs{
		width:750upx;
		padding:0upx 40upx;
		display:flex;
		justify-content:space-between;
		.tab-box{
			text{
				color:#fff;
				opacity: 0.5;
				font-size: 24upx;
				margin-right:40upx;
				padding:10upx 0upx;
				&.active{
					border-bottom:2upx solid #fff;
					opacity: 1;
					font-weight:bold;
				}
			}
		}
	}
	.fun-card-item{
		padding:20upx 30upx;
	}
	.fixed-btn{
		position: absolute;
		top:10upx;
		right:40upx;
		width:26upx;
		height:32upx;
	}
	.translist{
		padding:0upx 40upx;
		padding-top:10upx;
	}
	.horizon-list-item{
		padding:10upx 0upx;
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