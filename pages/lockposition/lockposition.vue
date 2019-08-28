<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="智能锁仓" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container">
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button value="自动锁仓" width="320upx" type="light" large></fun-button>
					<fun-button value="邀请好友锁仓" width="320upx" icon="../../static/icons/icon_invite.png" large></fun-button>
				</view>
			</view>
			<view class="wallet-banner">
				<image :src="imageLib.banner" alt="" />
			</view>
			<view style="padding:0px 40upx;padding-bottom:20upx;">
				<view class="fun-card">
					<view class="fun-card-item">
						<view style="position: relative;width:100%;text-align: center;font-size: 30upx;color:#fff;">
							锁仓总收益
							<fun-button value="账单" type="text" color="#DA53A2"
							style="position:absolute;top:-12upx;right:0upx;"></fun-button>
						</view>
						<view class="lock-total-box">
							<view class="lock-item-box">
								<view class="lock-item">
									<text style="font-size:56upx;color:#DA53A2;font-family: 'Montserrat-Bold';">6</text>
									<text style="font-size:28upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;">Forest</text>
								</view>
								<view class="lock-item">
									<text style="font-size:56upx;color:#DA53A2;font-family: 'Montserrat-Bold';">88</text>
									<text style="font-size:28upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;">Xdog</text>
								</view>
								<view class="lock-item-block">
									今日收益
								</view>
							</view>
							<view class="lock-item-vertical"></view>
							<view class="lock-item-box">
								<view class="lock-item">
									<text style="font-size:56upx;color:#DA53A2;font-family: 'Montserrat-Bold';">54</text>
									<text style="font-size:28upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;">Forest</text>
								</view>
								<view class="lock-item">
									<text style="font-size:56upx;color:#DA53A2;font-family: 'Montserrat-Bold';">452</text>
									<text style="font-size:28upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;">Xdog</text>
								</view>
								<view class="lock-item-block">
									累计收益
								</view>
							</view>
						</view>
					</view>
				</view>
				<view class="fun-card" style="margin-top:30upx;background: transparent;">
					<view class="fun-card-item">
						<view class="lock-total-box" style="padding:0upx;">
							<view class="lock-item-box">
								<view style="color:#fff;font-size: 28upx;text-align: center;padding:10upx;">今日收益</view>
								<view class="lock-item-block">
									<view class="lock-item">
										<text style="font-size:28upx;color:#fff;font-family: 'Montserrat-Bold';display: inline-block;padding:0upx 10upx;">2</text>
										<text style="font-size:24upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;display: inline-block;">Forest</text>
									</view>
									<view class="lock-item">
										<text style="font-size:28upx;color:#fff;font-family: 'Montserrat-Bold';display: inline-block;padding:0upx 10upx;">30</text>
										<text style="font-size:24upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;display: inline-block;">Xdog</text>
									</view>
									<view class="lock-item-block" style="font-size: 24upx;padding-top:6upx;">
										自主锁仓
									</view>
								</view>
								<view class="lock-item-block">
									<view class="lock-item">
										<text style="font-size:28upx;color:#fff;font-family: 'Montserrat-Bold';display: inline-block;padding:0upx 10upx;">2</text>
										<text style="font-size:24upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;display: inline-block;">Forest</text>
									</view>
									<view class="lock-item">
										<text style="font-size:28upx;color:#fff;font-family: 'Montserrat-Bold';display: inline-block;padding:0upx 10upx;">30</text>
										<text style="font-size:24upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;display: inline-block;">Xdog</text>
									</view>
									<view class="lock-item-block" style="font-size: 24upx;padding-top:6upx;">
										推广收益
									</view>
								</view>
							</view>
							<view class="lock-item-vertical" style="height:270upx;margin-top:20upx;"></view>
							<view class="lock-item-box">
								<view style="color:#fff;font-size: 28upx;text-align: center;padding:10upx;">累计收益</view>
								<view class="lock-item-block">
									<view class="lock-item">
										<text style="font-size:28upx;color:#fff;font-family: 'Montserrat-Bold';display: inline-block;padding:0upx 10upx;">20</text>
										<text style="font-size:24upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;display: inline-block;">Forest</text>
									</view>
									<view class="lock-item">
										<text style="font-size:28upx;color:#fff;font-family: 'Montserrat-Bold';display: inline-block;padding:0upx 10upx;">888</text>
										<text style="font-size:24upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;display: inline-block;">Xdog</text>
									</view>
									<view class="lock-item-block" style="font-size: 24upx;padding-top:6upx;">
										自主锁仓
									</view>
								</view>
								<view class="lock-item-block">
									<view class="lock-item">
										<text style="font-size:28upx;color:#fff;font-family: 'Montserrat-Bold';display: inline-block;padding:0upx 10upx;">20</text>
										<text style="font-size:24upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;display: inline-block;">Forest</text>
									</view>
									<view class="lock-item">
										<text style="font-size:28upx;color:#fff;font-family: 'Montserrat-Bold';display: inline-block;padding:0upx 10upx;">888</text>
										<text style="font-size:24upx;color:#999;font-family: 'Montserrat-Light';line-height: 48upx;display: inline-block;">Xdog</text>
									</view>
									<view class="lock-item-block" style="font-size: 24upx;padding-top:6upx;">
										推广收益
									</view>
								</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			<view class="lockpay-box">
				<view class="lock-tab">
					<view :class="['lock-tab-item',activeTab == 0?'active':'']">
						<text>锁仓收益</text>
					</view>
					<view :class="['lock-tab-item',activeTab == 1?'active':'']">
						<text>推广收益</text>
					</view>
				</view>
				<view class="lock-table">
					
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
					},
					textbtn:{
						text:'锁仓规则'
					}
				},
				imageLib:{
					message:'../../static/icons/message.png',
					union:'../../static/icons/Union.png',
					banner:'../../static/banner1.jpg'
				},
				activeTab:0
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
	}
</script>

<style lang="scss" scoped>
	.wallet-banner{
		width:750upx;
		padding:30upx 40upx;
		padding-top:174upx;
		position:relative;
		image{
			width:100%;
			height:520upx;
			display: block;
		}
	}
	.lock-total-box{
		width:100%;
		display:flex;
		justify-content:space-between;
		padding:20upx 0px;
		padding-top:40upx;
		.lock-item-vertical{
			width:2upx;
			background:rgba(255,255,255,0.1);
			height:108upx;
		}
		.lock-item-box{
			width:46%;
			display:flex;
			justify-content:space-around;
			flex-wrap:wrap;
			.lock-item-block{
				width:100%;
				text-align: center;
				padding-top:30upx;
				font-size: 28upx;
				color:#c7c7c7;
				display:flex;
				justify-content:space-around;
				flex-wrap:wrap;
			}
			.lock-item{
				width:50%;
				text-align:center;
				text{
					display: block;
				}
			}
		}
	}
	.lockpay-box{
		width:750upx;
		background: #000;
		margin-bottom:30upx;
		.lock-table{
			padding:20upx 40upx;
			
		}
		.lock-tab{
			border-bottom:2upx solid rgba(255,255,255,0.1);
			display:flex;
			justify-content:space-between;
			.lock-tab-item{
				width:50%;
				text-align:center;
				text{
					font-size:28upx;
					color:#fff;
					line-height:80upx;
					height:80upx;
					display: inline-block;
				}
				&.active text{
					border-bottom:2upx solid #fff;
				}
			}
		}
	}
</style>
