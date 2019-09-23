<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="场外交易" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="fiexd-btn" @click="openVip()">
			<image :src="imageLib.add"></image>
		</view>
		<view class="app-container full">
			<view class="radio-box noborder" style="width:750upx;padding:0px 235upx;">
				<text style="width:50%;" :class="{active:activeTab == 0}" @click="toggleTab(0)">买币</text>
				<text style="width:50%;" :class="{active:activeTab == 1}" @click="toggleTab(1)">卖币</text>
				<image class="fixed-btn" :src="imageLib.filter"></image>
			</view>
			<view class="fun-horizen" style="margin-top:30upx;"></view>
			<view class="transout-tabs">
				<view class="tab-box">
					<text class="active">USDT</text>
					<text>Xdag</text>
					<text>Forest</text>
				</view>
				<fun-button value="我的挂单" type="text" color="#DA53A2" url="../mybill/mybill"></fun-button>
			</view>
			<scroll-view scroll-y='true' style="width:100%;height:calc(100vh - 360upx);">
				<view class="fun-card" style="margin:20upx 40upx;">
					<view class="fun-card-item" style="text-align: center;padding:20upx;">
						<text style="color:#999;font-size: 26upx;">USDT 市场参考价</text>
						<text style="color:#DA53A2;font-size: 26upx;padding-left:15upx;font-weight: bold;">6.67 CNY</text>
					</view>
				</view>
				<view class="translist">
					<block v-for="(item,index) in transList" :key="index">
						<view class="fun-card" style="margin-bottom: 40upx;">
							<view class="fun-card-item">
								<view class="horizon-list-item">
									<view class="left-item">
										<image class="left-item-avatar" :src="imageLib.union"></image>
										<text class="left-item-name">美好即将发生</text>
									</view>
									<view class="right-item">
										<text>11单 · 61.11% 完成率</text>
									</view>
								</view>
								<view class="horizon-list-item">
									<view style="padding-top:15upx;">
										<view class="left-item">
											<text class="left-item-label">数量</text>
											<text class="left-item-name">10000</text>
										</view>
										<view class="left-item" style="padding-top:20upx;">
											<text class="left-item-label">限额</text>
											<text class="left-item-name">668.68-66868</text>
										</view>
									</view>
									<view class="right-item" style="display: block;margin-top:20upx;">
										<view style="text-align: right;color:#fff;">单价</view>
										<view style="text-align: right;padding-top:10upx;font-size: 32upx;color:#fff;font-family: 'Montserrat-Bold';">
											<span style="font-size: 24upx;display: inline-block;padding-right:10upx">¥</span>
											 6.6868
										</view>
									</view>
								</view>
							</view>
							<view class="fun-horizen"></view>
							<view class="fun-card-item">
								<view class="horizon-list-item">
									<view class="left-item">
										<image style="width:24upx;height:24upx;" class="left-item-avatar" :src="imageLib.alipay"></image>
										<image style="width:24upx;height:24upx;" class="left-item-avatar" :src="imageLib.wechatpay"></image>
										<image style="width:40upx;height:24upx;" class="left-item-avatar" :src="imageLib.unionpay"></image>
									</view>
									<view class="right-item">
										<fun-button value="购买" width="220upx" url="../buyusdt/buyusdt"></fun-button>
									</view>
								</view>
							</view>
						</view>
					</block>
				</view>
			</scroll-view>
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
				activeTab:1,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},
					textbtn:{
						text:'订单记录',
						url:'../ordernotes/ordernotes'
					}
				},
				imageLib:{
					filter:'../../static/icons/filter.png',
					union:'../../static/avatar/fortoken.png',
					alipay:'../../static/icons/icon_alipay.png',
					wechatpay:'../../static/icons/icon_wechatpay.png',
					unionpay:'../../static/icons/icon_unionpay.png',
					add:'../../static/icons/icon_add.png',
				},
				activeTab:0,
				transList:[
					{},{},{}
				],
				isVip:true
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			tabChange(value){
				this.activeTab = value.detail.current;
			},
			toggleTab(index){
				this.activeTab = index;
			},
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
	.swiper-box{
		height:calc(100vh - 356upx);
	}
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
				padding:12upx 0upx;
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
	.horizon-list-item{
		padding:10upx 0upx !important;
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
			}
			.left-item-label{
				color:#999;
				font-size: 24upx;
				margin-right: 18upx;
			}
		}
		.right-item{
			display:flex;
			justify-content:flex-end;
			align-items:center;
			color:#999;
			font-size: 24upx;
		}
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
		.horizon-list-item{
			padding:20upx 40upx;
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
					font-family:'Montserrat-Light';
				}
			}
			.right-item{
				width:300upx;
				display: flex;
				justify-content: flex-end;
				align-items: center;
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
	}
</style>