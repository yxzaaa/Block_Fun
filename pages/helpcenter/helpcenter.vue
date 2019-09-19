<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			title="帮助中心" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container">
			<view style="font-size: 16px;color:#fff;margin:0upx 30upx 0;">一、钱包板块</view>
			<view class="helpbox">
				<view class="help">
					<span class="title">1.钱包转让</span>
					<span class="method">
						<span>如何进行收款与转账？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method">
						<span>支付密码怎么修改？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method">
						<span>费率相关</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method">
						<span>转账失败怎么办？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method" style="border-bottom:none;">
						<span>其他</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
				</view>
				<view class="help" style="margin-top:44upx;">
					<span class="title">2.智能锁仓</span>
					<span class="method">
						<span>怎么看到我的锁仓收益？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method">
						<span>收益怎么结算，何时发放？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method">
						<span>不想锁仓了，可以申请提前解锁吗？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method">
						<span>我邀请好友，有人数限制吗？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method" style="border-bottom:none;">
						<span>其他</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
				</view>
				<view class="help" style="margin-top:44upx;">
					<span class="title">3.借贷相关</span>
					<span class="method">
						<span>费率</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method">
						<span>我的借贷有效期多久</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method">
						<span>违约协议</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method">
						<span>借贷协议</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method" style="border-bottom:none;">
						<span>其他</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
				</view>
			</view>
			<view style="font-size: 16px;color:#fff;margin:34upx 30upx 0;">二、矿池板块</view>
			<view class="helpbox" style="width:690upx;height:632upx;">
				<view class="help" style="">
					<span class="title">1.闪挖</span>
					<span class="method">
						<span>什么是闪挖？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method" style="border:none;">
						<span>VIP与SVIP的区别？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
				</view>
				<view class="help" style="margin-top:46upx;">
					<span class="title">2.我的矿池</span>
					<span class="method">
						<span>矿机怎么配置？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
					<span class="method" style="border:none;">
						<span>怎么增加算力？</span>
						<image src="../../static/bg/right2.png"></image>
					</span>
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
					textbtn:{
						text:'我要反馈',
						
					}
				}
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods: {
			
		}
	}
</script>

<style lang='scss' scoped>
	.helpbox{
		width:690upx;
		height:1908upx;
		background: #2D1F25;
		border-radius: 8upx;
		margin:34upx 30upx 54upx;
		padding:54upx 30upx 46upx;
		.title{
			font-size: 30upx;	
			color: #FFFFFF;
			opacity: 0.5;
			margin-bottom:40upx;
			display:block;
		}
		.method{
			display: flex;
			justify-content: space-between;
			align-items: flex-start;
			width:630upx;
			height:75upx;
			border-bottom:1px solid rgba(255,255,255,0.1);
			margin-top:34upx;
			span{
				font-size: 28upx;
				color: #FFFFFF;
			}
			image{
				width:12upx;
				height:22upx;
			}
		}
		
	}
</style>
