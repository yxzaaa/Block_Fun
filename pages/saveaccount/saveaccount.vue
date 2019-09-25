<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="收款" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<div class="app-container full">
			<view class="status-box" style="padding:20upx 40upx;">
				<view class="left-status">
					<image :src="imageLib.logosmall" style="width:40upx;height:40upx;" />
					<text style="font-size:30upx;font-family:'Montserrat-Light';color:#fff;">Forbidden {{coin}} Coin</text>
					<text style="font-size:26upx;color:#999;">{{coin}}</text>
				</view>
			</view>
			<view class="fun-card" style="margin:30upx 40upx;width:670upx;">
				<view class="fun-card-item">
					<text style="font-size: 24upx;color:#999;">注意：该地址只接收{{coin}}资产，如充值其他币种，将无法找回</text>
				</view>
				<view class="fun-horizen"></view>
				<view class="fun-card-item">
					<view class="erweima">
						<image :src="erweima"></image>
					</view>
				</view>
				<view class="fun-card-item" style="padding-top:10upx;">
					<view 
						style="color:#fff;font-family:'Montserrat-Bold';font-size:24upx;text-align: center;padding-bottom:20upx;"
					>
						1gmHhylYGlhyHLhlkgesLmncXWibFAWohJD
					</view>
					<view style="display:flex;justify-content: center;">
						<fun-button 
							type="text" 
							color="#DA53A2" 
							icon="/static/icons/copy.png" 
							value="复制地址" 
							large
							width="200upx"
						/>
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
				imageLib:{
					logosmall:'../../static/icons/logo_small.png'
				},
				erweima:'../../static/image.png',
				coin:''
			};
		},
		onLoad(option){
			this.coin = option.coin;
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
		padding:20upx 0;
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
		padding:30upx 0;
		text{
			color:#DA53A2;
			font-size: 52upx;
			font-family:'Montserrat-Bold';
		}
	}
	.erweima{
		width:280upx;
		height:280upx;
		background: #fff;
		border-radius: 12upx;
		margin:auto;
		padding:30upx;
		image{
			width:100%;
			height:100%;
		}
	}
</style>
