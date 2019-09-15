<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			title="安全中心" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full">
			<view class="savebox">
				<navigator url="../amendpaypassword/amendpaypassword">
					<view class="design">
						<view class="left">
							<image src="../../static/bg/password.png"></image>
							<span>支付密码</span>
						</view>
						<view class="right">
							<span>修改</span>
							<image src="../../static/bg/right.png"></image>
						</view>
					</view>
					<view class="item-horizen"></view>
				</navigator>
				<navigator url="../forgetpaypassword/forgetpaypassword">
					<view class="design">
						<view class="left">
							<image src="../../static/bg/lock.png"></image>
							<span>登录密码</span>
						</view>
						<view class="right">
							<span>修改</span>
							<image src="../../static/bg/right.png"></image>
						</view>
					</view>
					<view class="item-horizen"></view>
				</navigator>
				<view class="design">
					<view class="left">
						<image src="../../static/bg/finger.png"></image>
						<span>指纹登录</span>
					</view>
					<view class="right">
						<span>设置</span>
						<image src="../../static/bg/right.png"></image>
					</view>
				</view>
				<view class="item-horizen"></view>
				<view class="design">
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
			UniBackground
		},
		data() {
			return {
				scroll:0,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},		
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

<style lang="scss" scoped>
	.savebox{
		width:670upx;
		background: #2D1F25;
		border-radius: 8upx;
		margin:0px 40upx;
		display: flex;
		flex-direction: column;
		justify-content: space-between;	
		.item-horizen{
			width:610upx;
			height:2upx;
			background: rgba(255,255,255,0.2);
			margin:0px 30upx;
		}
		.design{
			display: flex;
			justify-content: space-between;
			align-items: flex-start;
			// margin-bottom: 39upx;
			width:670upx;
			padding:40upx 30upx;
			.left{
				display: flex;
				align-items: center;
				justify-content: space-between;
				image{
					width:36upx;
					height:36upx;
					margin-right: 40upx;					
				}
				span{
					font-size:28upx;
					color: #fff;
				}
			}
			.right{
				display: flex;
				align-items: center;
				justify-content: space-between;
				image{
					width:30upx;
					height:30upx;					
				}
				span{
					margin-right: 16upx;
					font-size: 24upx;
					color: #FFFFFF;
					opacity: 0.5;
				}				
			}
		}
	}
</style>
