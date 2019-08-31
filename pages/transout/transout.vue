<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="场外交易" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="radio-box noborder" style="width:750upx;padding:0px 235upx;">
				<text style="width:50%;" class="active">买币</text>
				<text style="width:50%;">卖币</text>
				<image class="fixed-btn" :src="imageLib.filter"></image>
			</view>
			<view class="fun-horizen" style="margin-top:30upx;"></view>
			<view class="transout-tabs">
				<view class="tab-box">
					<text class="active">USTD</text>
					<text>Xdag</text>
					<text>Forest</text>
				</view>
			</view>
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
					},
					textbtn:{
						text:'订单记录',
						url:'../lockrule/lockrule'
					}
				},
				imageLib:{
					filter:'../../static/icons/filter.png'
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
	.transout-tabs{
		width:750upx;
		padding:0upx 30upx;
		.tab-box{
			text{
				color:#fff;
				opacity: 0.5;
				font-size: 24upx;
				margin-right:40upx;
				padding:10upx 0upx;
				&.active{
					border-bottom:2upx solid #fff;
					opacity: 1;
					font-weight:bold;
				}
			}
		}
	}
	.fixed-btn{
		position: absolute;
		top:10upx;
		right:40upx;
		width:26upx;
		height:32upx;
	}
</style>