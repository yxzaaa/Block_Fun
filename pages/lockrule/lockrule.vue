<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="锁仓规则" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container">
			<view class="wallet-banner">
				<image :src="imageLib.banner" />
			</view>
		</view>
		<view class="section-header">
			<image :src="imageLib.prenote" class="section-icon"></image>
			<text class="section-title">锁仓前提</text>
		</view>
		<view class="section-header">
			<image :src="imageLib.locktype" class="section-icon"></image>
			<text class="section-title">锁仓类型</text>
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
					}
				},
				imageLib:{
					message:'../../static/icons/message.png',
					union:'../../static/icons/Union.png',
					banner:'../../static/banner2.jpg',
					prenote:'../../static/icons/icon_pre.png',
					locktype:'../../static/icons/icon_type.png',
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
</style>
