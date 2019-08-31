<template>
	<view>
		<uni-background />
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
					<span style="font-size:24upx;font-family: Montserrat-bold;color:#999999;border:1px solid #999999;padding:4upx 20upx;">一键复制</span>
				</span>
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
				font-weight: 600;
				font-size: 32upx;
				color:#fff;
			}
		}
	}
</style>
