<template>
	<view>
		<uni-background :src="imageLib.bg"/>
		<uni-nav-bar 
			:opacity="scroll"
			title="我的"
			textColor="#fff"
		/>
		<view class="user-info">
			<image src="../../static/bg/logo.png" style="width:120upx;height:120upx;"></image>
			<view class="info">
				<span class="id">13936525463</span>
				<span class="users" style="margin-top:30upx;">
					<span class="user" style="margin-right:44upx;font-size:24upx;font-family: Montserrat-bold;color:#999999;">
						UID：100001
					</span>
					<span style="font-size:24upx;color:#999999;border:1px solid #999999;padding:4upx 20upx;border-radius: 6upx;">一键复制</span>
				</span>
			</view>
		</view>
		<view class="activity">
			<view class="active">
				<view>
						<image src="../../static/bg/task.png"></image>
						<span>每日任务</span>
				</view>
				<view>
					<image src="../../static/bg/friends.png"></image>
					<span>我的好友</span>
				</view>
				<view>
					<image src="../../static/bg/invite.png"></image>
					<span>邀请好友</span>
				</view>
			</view>
		</view>
		<view class="managebox">
			<view class="manage">
				<span class="title">订单管理</span>
				<view>
					<span class="goodsinfo">
						<span class="number">5</span>
						<span class="text">条订单信息</span>
					</span>
					<image src="../../static/bg/message.png" style="width:72upx;height:72upx;"></image>
				</view>
			</view>
			<view class="manage">
				<span class="title">购物车</span>
				<view>
					<span class="goodsinfo">
						<span class="number">1</span>
						<span class="text">条商品信息</span>
					</span>
					<image src="../../static/bg/cart.png" style="width:72upx;height:72upx;"></image>
				</view>
			</view>
		</view>
		<view class="managebox">
			<view class="manage">
				<span class="title">收藏夹</span>
				<view>
					<span class="goodsinfo">
						<span class="number">5</span>
						<span class="text">条收藏信息</span>
					</span>
					<image src="../../static/bg/sign.png" style="width:72upx;height:72upx;"></image>
				</view>
			</view>
			<view class="manage">
				<span class="title">在线客服</span>
				<view>
					<span class="goodsinfo">
						<span class="number">5</span>
						<span class="text">条客服信息</span>
					</span>
					<image src="../../static/bg/service.png" style="width:72upx;height:72upx;"></image>
				</view>
			</view>
		</view>
		<view class="action">
			<view class="action-item">
				<view>
					<image src="../../static/bg/finance.png"></image>
					<span>我的财务</span>
				</view>
				<image src="../../static/bg/jiantou.png"></image>
			</view>
			<view class="action-item">
				<view>
					<image src="../../static/bg/realname.png"></image>
					<span>实名认证</span>
				</view>
				<image src="../../static/bg/jiantou.png"></image>
			</view>
			<view class="action-item">
				<view>
					<image src="../../static/bg/save.png"></image>
					<span>安全中心</span>
				</view>
				<image src="../../static/bg/jiantou.png"></image>
			</view>
			<view class="action-item">
				<view>
					<image src="../../static/bg/help.png"></image>
					<span>帮助中心</span>
				</view>
				<image src="../../static/bg/jiantou.png"></image>
			</view>
			<view class="action-item" style="border:none;margin-bottom: 0;">
				<view>
					<image src="../../static/bg/about.png"></image>
					<span>关于我们</span>
				</view>
				<image src="../../static/bg/jiantou.png"></image>
			</view>
		</view>
		<view class="exit">
			退出登录
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
		},
		data() {
			return {
				scroll:0,
				imageLib:{
					bg:'../../static/bg2.jpg'
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
		display: flex;
		width:490upx;
		height:120upx;
		margin-top:216upx;
		margin-left:40upx;
		justify-content:space-between;
		.info{
			display: flex;
			flex-direction: column;
			.id{
				font-family: Montserrat-bold;
				font-style: normal;
				font-size: 32upx;
				color:#fff;
			}
		}
	}
	.activity{
		width:670upx;
		height:180upx;
		margin:64upx 40upx 0;
		background-image:url(../../static/bg3.jpg);
		background-size:100% 100%;
		border-radius: 12upx;
		padding:28upx 64upx 22upx;
		.active{
			display: flex;
			justify-content:space-between;
			
			view{
				display: flex;
				flex-direction: column;
				justify-content:center;
				
				image{
					margin-left:2upx;
					width:88upx;
					height:88upx;
					margin-bottom: 8upx;
				}
				span{
					font-size:24upx;
					color: #DA53A2;
				}
				
			}
		}
		
	}
	.managebox{
		width:670upx;
		height:200upx;
		margin:40upx 40upx 30upx;
		display:flex;
		justify-content:space-between;
		.manage{
			background: #2D1F25;
			opacity: 0.8;
			padding:40upx;
			width:46%;
			height:200upx;
			border-radius:8upx;
			.title{
				
				font-size: 28upx;
				color:#fff;
				font-weight: bold;
			}
			view{
				display: flex;
				justify-content:space-between;
				align-items: flex-start;
				margin-top:8upx;
				.goodsinfo{
					display: flex;
				}
				.number{
					margin-right:12upx;
					display: block;
					color: #DA53A2;
					font-family: 'Montserrat-Bold';
					font-style: normal;
					font-weight: 600;
					font-size: 24upx;
				}
				.text{
					color:#999999;
					font-size: 24upx;
				}
			}
		}
	}
	.action{
		width:670upx;
		height:600upx;
		background: #2D1F25;
		opacity: 0.8;
		border-radius: 8upx;
		margin:40upx 40upx 0;
		padding:40upx 30upx;
		.action-item{
			display:flex;
			width:610upx;
			height:81upx;
			border-bottom:1px solid rgba(255,255,255,0.1);
			justify-content:space-between;
			margin-bottom:39upx;
			view{
				display:flex;
				justify-content:space-between;
				image{
					width:36upx;
					height:36upx;
					margin-right:40upx;
					
				}
				span{
					font-size:28upx;
					color: #fff;
					font-family: PingFang SC;
				}
			}
			image{
				width:26upx;
				height:26upx;
				margin-top: 6upx;
				margin-right:4upx;
			}
		}
	}
	.exit{
		width:670upx;
		height:88upx;
		margin:80upx 40upx;
		background: #2D1F25;
		opacity: 0.8;
		border-radius: 4px;
		text-align: center;
		line-height: 88upx;
		font-size:28upx;
		color:#fff;
	}
</style>
