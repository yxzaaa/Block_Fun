<template>
	<view>
		<uni-background />
		<uni-nav-bar 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full">
			<view style="width:288upx;height:68upx;line-height:68upx;margin:0 40upx 0;color:#fff;font-family: PingFang SC;font-size: 48upx;">
				修改支付密码
			</view>
			<view style="width:224upx;height:40upx;line-height:40upx;margin:20upx 40upx 0;color:#fff;font-family: PingFang SC;font-size: 28upx;">请输入原支付密码</view>
			
			<view style="margin:0 40upx;color:#DA53A2;font-family: PingFang SC;font-size: 28upx;">忘记密码？</view>
			<fun-button value="提交" block large width="670upx"></fun-button>
		</view>
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
	.input{
		width:750upx;
		height:94upx;
		padding:0 46upx 0 40upx; 
		margin:40upx 0;
		display:flex;
		justify-content:space-between;
		view{
			width:94upx;
			height:94upx;
			background:#fff;
			opacity: 0.1;
			border-radius: 4upx;
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
