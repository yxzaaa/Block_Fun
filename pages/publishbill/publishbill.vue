<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="发布挂单" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view style="padding:0upx 40upx;padding-bottom:30upx;">
				<view class="fun-card" style="margin-bottom:30upx;">
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item"><text class="left-item-name">交易类型</text></view>
							<view class="right-item" style="width:272upx;height:48upx;">
								<view class="radio-box">
									<text style="width:50%;" class="active">购买</text>
									<text style="width:50%;">出售</text>
								</view>
							</view>
						</view>
					</view>
				</view>
				<view class="fun-card" style="margin-bottom:30upx;">
					<view class="fun-card-item">1</view>
				</view>
				<view class="fun-card" style="margin-bottom:30upx;">
					<view class="fun-card-item">1</view>
				</view>
				<view class="fun-card">
					<view class="fun-card-item">1</view>
				</view>
			</view>
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
					}
				},
				isVip:false,
				imageLib:{
					goldbg:'../../static/gold_btn.jpg',
					checked:'../../static/icons/checked.png'
				}
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			openVip(){
				uni.showModal({
					title:'购买 SVIP 会员',
					content:'您即将购买SVIP会员，我们将从您的钱包中直接扣除199USDT，会员有效期一年。',
					success:res=>{
						console.log(res);
						if(res.confirm){
							
						}else if(res.cancel){
							
						}
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.fun-card-item{
		padding:30upx 40upx;
	}
	.horizon-list-item{
		padding:10upx 0upx;
		display:flex;
		justify-content:space-between;
		align-items:center;
		.left-item{
			display:flex;
			justify-content:flex-start;
			align-items:center;
			.left-item-avatar{
				width:40upx;
				height:40upx;
				margin-right:20upx;
			}
			.left-item-name{
				color:#fff;
				font-size: 26upx;
			}
			.left-item-label{
				color:#999;
				font-size: 24upx;
				margin-right: 18upx;
			}
		}
		.right-item{
			display:flex;
			justify-content:flex-end;
			align-items:center;
			color:#999;
			font-size: 24upx;
		}
	}
	
</style>
