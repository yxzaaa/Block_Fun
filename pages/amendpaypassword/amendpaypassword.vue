<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full" style="padding-left:40upx;padding-right:40upx;">
			<view style="width:670upx;line-height:68upx;color:#fff;font-size: 48upx;">
				修改支付密码
			</view>
			<view style="line-height:40upx;color:#fff;font-size: 28upx;padding-top:30upx;">请输入原支付密码</view>
			<view style="width:670upx;padding-top:60upx;">
				<possword-inputer size="74upx" borderColor="rgba(255,255,255,0.4)" fontSize="48upx"></possword-inputer>
			</view>
			<view style="color:#DA53A2;font-size: 28upx;padding-top:30upx;padding-bottom:80upx;">忘记密码？</view>
			<fun-button value="提交" block large width="670upx"></fun-button>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import FunButton from '@/components/fun-button.vue';
	import PosswordInputer from '@/components/possword-inputer.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			FunButton,
			PosswordInputer
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
