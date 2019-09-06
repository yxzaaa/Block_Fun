<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="我的挂单" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="fun-card" style="margin:20upx 40upx;">
				<view class="fun-card-item">
					<view class="horizon-list-item">
						<view class="left-item" style="width:420upx;">
							<text class="left-item-name">广告在线</text>
							<text style="font-size: 24upx;color:#999;padding-left:10upx;">开启时才会显示已上架广告</text>
						</view>
						<view class="right-item" style="width:96upx;height:48upx;">
							<view class="check-box" @click="showAd = showAd?false:true">
								<text :class="{active:showAd}"></text>
							</view>
						</view>
					</view>
				</view>
			</view>
			<view class="translist">
				<block v-for="(item,index) in transList" :key="index">
					<view class="fun-card" style="margin-bottom: 40upx;">
						<view class="fun-card-item">
							<view class="horizon-list-item">
								<view class="left-item" style="width:500upx;">
									<image class="left-item-avatar" style="margin-right:5upx;" :src="item.sold?imageLib.sold:imageLib.bought"></image>
									<text class="left-item-name" :style="{color:item.sold?'#56CCF2':'#DA53A2'}">{{item.sold?'出售':'购买'}}</text>
									<text class="left-item-label">|</text>
									<text class="left-item-name">浮动价</text>
									<text class="left-item-label">|</text>
									<text class="left-item-name">USDT</text>
									<image style="width:24upx;height:24upx;" class="left-item-avatar" :src="imageLib.alipay"></image>
								</view>
								<view class="right-item">
									<text class="left-item-name" style="color:#fff;">已发布</text>
								</view>
							</view>
							<view class="horizon-list-item" style="padding-top:20upx;">
								<view class="left-item">
									<text class="left-item-label">单价</text>
								</view>
								<view class="right-item">
									<text class="left-item-name">6.6868 CNY</text>
								</view>
							</view>
							<view class="horizon-list-item" style="padding-top:20upx;">
								<view class="left-item">
									<text class="left-item-label">限量USDT</text>
								</view>
								<view class="right-item">
									<text class="left-item-name">100 - 1000</text>
								</view>
							</view>
						</view>
						<view class="fun-horizen"></view>
						<view class="fun-card-item">
							<view class="horizon-list-item">
								<view class="left-item">
									<text class="left-item-label">14天后过期</text>
								</view>
								<view class="right-item">
									<fun-button :value="item.sold?'上架':'下架'" width="220upx" :background="item.sold?'#56CCF2':'#DA53A2'"></fun-button>
								</view>
							</view>
						</view>
					</view>
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
					filter:'../../static/icons/filter.png',
					sold:'../../static/icons/icon_sold.png',
					bought:'../../static/icons/icon_bought.png',
					alipay:'../../static/icons/icon_alipay.png',
					wechatpay:'../../static/icons/icon_wechatpay.png',
					unionpay:'../../static/icons/icon_unionpay.png',
					add:'../../static/icons/icon_add.png',
				},
				activeTab:0,
				transList:[
					{
						sold:false,
					},
					{
						sold:true,
					}
				],
				isVip:true,
				showAd:true
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			openVip(){
				if(this.isVip){
					uni.navigateTo({
						url:'../publishbill/publishbill'
					})
				}else{
					uni.showModal({
						title:'您当前没有发布挂单资格',
						content:'升级为SVIP用户后，即可享有挂单资格',
						confirmText:'去升级',
						success:res=>{
							console.log(res);
							if(res.confirm){
								uni.navigateTo({
									url:'../paysvip/paysvip'
								})
							}else if(res.cancel){
								
							}
						}
					})
				}
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