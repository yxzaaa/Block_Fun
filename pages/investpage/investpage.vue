<template>
	<view class="container">
		<uni-background src="../../static/bg1.jpg"/>
		<uni-nav-bar title="我要投资" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<div class="app-container full fixbutton">
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button 
						value="确定投资" 
						width="670upx"  
						large 
					></fun-button>
				</view>
			</view>
			<view class="user-info" style="padding-top:40upx;">
				<text>总利息</text>
			</view>
			<view class="user-count">
				<text style="font-family: 'Montserrat-Bold';font-size:64upx;">12</text>
				<text>USDT</text>
			</view>
			<view class="user-info">
				<text style="color:rgba(255,255,255,0.5);font-size: 26upx;">月利率0.1%</text>
			</view>
			<view style="padding:40upx;">
				<view class="fun-card">
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">Forest 单价</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">0.168 USDT/X</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">投资总量</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">800 USDT</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">投资周期</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">15 天</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">抵押总量</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">10000</text>
							</view>
						</view>
						<!-- <view class="horizon-list-item">
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
								<text class="left-item-name">0.8 USDT</text>
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
	export default {
		components:{
			UniNavBar,
			UniBackground,
			FunButton
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
				}
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
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
