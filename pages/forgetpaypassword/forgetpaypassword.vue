<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full"></view>
		<view style="margin:0upx 40upx 0;color:#fff;font-family: PingFang SC;font-size: 48upx;">忘记支付密码</view>
		<view class="textbox">
			<view class="text">
				<span class="number">手机号</span>
				<view>
					<input type="text" value="请输入手机号">
					<span>发送验证码</span>
				</view>
			</view>
			<view class="text" style="margin-top:61upx;">
				<span class="number" style="margin-top:61upx;">验证码</span>
				<view>
					<input type="text" value="请输入手机号">
				</view>
			</view>
		</view>
		<view class="commit">确认</view>
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
	.textbox{
		width:670upx;
		height:442upx;
		margin:40upx;
		padding:42upx 40upx 61upx;
		background: #2D1F25;
		opacity: 0.8;
		box-shadow: 0px 8upx 20upx rgba(43, 114, 251, 0.05);
		border-radius: 4px;
		.text{
			width:590upx;
			height:139upx;
			border-bottom:1px solid rgba(255,255,255,0.1);
			.number{
				font-family: PingFang SC;
				font-size: 28upx;
				color:#fff;
			}
			view{
				margin-top:34upx;
				display:flex;
				justify-content:space-between;
				align-items:center;
				input{
					width:300upx;
					color: #FFFFFF;
					opacity: 0.5;
					font-family: PingFang SC;
					font-size: 24upx;
				}
				span{	
					color: #DA53A2;
					font-family: PingFang SC;
					font-size: 24upx;
				}
			}
		}
	}
	.commit{
		width:670upx;
		height:80upx;
		margin:80upx 40upx;
		background:#DA53A2;
		text-align: center;
		line-height:80upx;
		color:#fff;
		font-size: 28upx;
		border-radius: 2000upx;
	}
</style>
