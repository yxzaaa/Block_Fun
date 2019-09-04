<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="订单详情" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view style="padding:0upx 40upx">
				<view class="fun-card">
					<view class="fun-card-item" style="padding:20upx;">
						<view class="horizon-list-item" style="justify-content: center;">
							<text style="color:rgba(255,255,255,0.5);font-size:24upx;">对方将订单标记为 "已支付"，请尽快点击【放行】</text>
						</view>
					</view>
				</view>
				<view class="main-title" style="text-align: left;">进行中</view>
				<view class="fun-horizen" style="margin-bottom:20upx;"></view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">订单编号</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">2A4EF9Q3FA8WDAMW19Z668PAFR</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">创建时间</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">2019/01/28 20:35</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">价格</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">6.6868 CNY</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">限额</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">100 USDT</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">总金额</text>
					</view>
					<view class="right-item">
						<text style="font-size: 40upx;color:#fff;font-family: 'Montserrat-Bold';">668.68 CNY</text>
					</view>
				</view>
				<view class="fun-card" style="margin-top:20upx;">
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item">
								<image class="left-item-avatar" :src="imageLib.union"></image>
								<text class="left-item-name">美好即将发生</text>
							</view>
							<view class="right-item">
								<view class="button-group" style="width:280upx;">
									<fun-button icon="../../static/icons/icon_call.png" large width="132upx"></fun-button>
									<fun-button icon="../../static/icons/icon_contact.png" large width="132upx"></fun-button>
								</view>
							</view>
						</view>
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
					union:'../../static/avatar/fortoken.png',
				}
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
		}
	}
</script>

<style lang="scss" scoped>
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
				padding-right:15upx;
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