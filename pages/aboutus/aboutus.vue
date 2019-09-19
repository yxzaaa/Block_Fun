<template>
	<view class="container">
		<uni-background :src="imageLib.bg"/>
		<uni-nav-bar 
			title="关于我们" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full">
			<view style="width:124upx;height:124upx;margin:0upx 316upx 32upx;">
				<image src="../../static/bg/logo.png" style="width:124upx;height:124upx;"></image>
			</view>
			<view style="margin:0 310upx 12upx;color:#fff;font-weight: 600;font-size: 28upx;">Blockfun</view>
			<view style="margin:0 346upx 28upx;font-size: 24upx;color:#fff;width:60upx;height:24upx;">V1.0.1</view>
			<view style="width:670upx;height:240upx;color:#fff;font-size: 26upx;margin:0 40upx 90upx;line-height: 48upx;">Blockfun，是一款专门为Forest/Xdag这类优质创新资产而生的矿池全生态产品，产品涵盖移动轻钱包、矿池管理、矿机购买、云算力租赁、闪电挖矿、智能锁仓、场外交易、抵押借贷等，努力为矿工用户们提供更加全面高效的矿圈全场景服务。</view>
			<view class="savebox">
				<view class="design">
					<view class="left">
						<image src="../../static/bg/letter.png"></image>
						<span>邮箱</span>
					</view>
					<view class="right">
						<span>Blockfun@google.com</span>
						<image src="../../static/bg/right.png"></image>
					</view>
				</view>
				<view class="design">
					<view class="left">
						<image src="../../static/bg/text.png"></image>
						<span>用户协议</span>
					</view>
					<view class="right">
						<image src="../../static/bg/right.png"></image>
					</view>
				</view>
				<view class="design">
					<view class="left">
						<image src="../../static/bg/default.png"></image>
						<span>隐私协议</span>
					</view>
					<view class="right">
						<image src="../../static/bg/right.png"></image>
					</view>
				</view>
				<view class="design" style="border:none;height:42upx;">
					<view class="left">
						<image src="../../static/bg/load.png"></image>
						<span>版本更新</span>
					</view>
					<view class="right">
						<span>已经是最新的版本</span>
						<image src="../../static/bg/right.png"></image>
					</view>
				</view>
			</view>
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
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},		
				},
				imageLib:{
					bg:'../../static/bg2.jpg'
				},
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods: {
			
		}
	}
</script>

<style lang="scss" scoped>
	.savebox{
		width:670upx;
		height:482upx;
		background: #2D1F25;
		border-radius: 4px;
		margin:0 40upx;
		padding:40upx 30upx;
		display: flex;
		flex-direction: column;
		justify-content: space-between;	
		.design{
			display: flex;
			justify-content: space-between;
			align-items: flex-start;
			// margin-bottom: 39upx;
			width:610upx;
			height:81upx;
			border-bottom:1px solid rgba(255,255,255,0.1);
			.left{
				display: flex;
				align-items: center;
				justify-content: space-between;
				image{
					width:36upx;
					height:36upx;
					border:1px dashed rgba(255,255,255,0.5);
					margin-right: 40upx;					
				}
				span{
					font-size:28upx;
					color: #FFFFFF;
				}
			}
			.right{
				display: flex;
				align-items: center;
				justify-content: space-between;
				image{
					width:26upx;
					height:26upx;					
				}
				span{
					margin-right: 24upx;
					font-size: 24upx;
					color: #FFFFFF;
					opacity: 0.5;
				}				
			}
		}
	}
</style>
