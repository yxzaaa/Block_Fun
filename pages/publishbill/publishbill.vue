<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="发布挂单" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full fixbutton">
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button 
						value="发布" 
						width="670upx"  
						large 
						icon="../../static/icons/icon_send.png"
						@handle="openVip()"
					></fun-button>
				</view>
			</view>
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
						<view class="horizon-list-item">
							<view class="left-item"><text class="left-item-name">币种</text></view>
							<view class="right-item" style="height:48upx;">
								<text>USDT</text>
								<image :src="imageLib.more"></image>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item"><text class="left-item-name">法币</text></view>
							<view class="right-item" style="height:48upx;">
								<text>CNY</text>
								<image :src="imageLib.more"></image>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item"><text class="left-item-name">付款方式</text></view>
							<view class="right-item" style="height:48upx;">
								<text>请选择</text>
								<image :src="imageLib.more"></image>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item"><text class="left-item-name">付款期限</text></view>
							<view class="right-item" style="height:48upx;">
								<text>15分钟</text>
								<image :src="imageLib.more"></image>
							</view>
						</view>
					</view>
				</view>
				<view class="fun-card" style="margin-bottom:30upx;">
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item"><text class="left-item-name">定价方式</text></view>
							<view class="right-item" style="width:272upx;height:48upx;">
								<view class="radio-box">
									<text style="width:50%;" class="active">浮动价</text>
									<text style="width:50%;">一口价</text>
								</view>
							</view>
						</view>
						<view class="horizon-list-item" style="padding:20upx 0upx;">
							<view class="left-item">
								<text class="left-item-name">设置溢价</text>
								<text style="font-size: 24upx;color:#999;padding-left:14upx;">选填</text>
							</view>
							<view class="right-item" style="height:48upx;">
								<input type="text" placeholder="建议-10 ~ 0" style="font-size: 24upx;width:150upx;">
								<text style="color:#DA53A2">%</text>
							</view>
							<view style="width:100%;height:2upx;background: rgba(255,255,255,0.2);margin:10upx 0upx;"></view>
							<view class="left-item">
								<text style="font-size: 24upx;color:#999;">市场参考价 6.6758</text>
							</view>
							<view class="right-item" style="height:48upx;">
								<text style="color:#DA53A2">浮动价 6.1234</text>
							</view>
						</view>
						<view class="horizon-list-item" style="padding:20upx 0upx;">
							<view class="left-item">
								<text class="left-item-name">最高单价</text>
							</view>
							<view class="right-item" style="height:48upx;">
								<text style="color:#DA53A2;font-weight: bold;">39457.987 CNY</text>
							</view>
							<view style="width:100%;height:2upx;background: rgba(255,255,255,0.2);margin:10upx 0upx;"></view>
							<view class="left-item">
								<text style="font-size: 24upx;color:#999;">价格浮动到该价格以上，则不予成交</text>
							</view>
						</view>
					</view>
				</view>
				<view class="fun-card" style="margin-bottom:30upx;">
					<view class="fun-card-item">
						<view class="horizon-list-item" style="padding:20upx 0upx;">
							<view class="left-item"><text class="left-item-name">购买定量的USDT</text></view>
							<view class="right-item" style="width:272upx;height:48upx;">
								<view class="radio-box">
									<text style="width:50%;" class="active">定额</text>
									<text style="width:50%;">定价</text>
								</view>
							</view>
						</view>
						<view class="horizon-list-item" style="padding:20upx 0upx;">
							<view class="left-item">
								<input type="text" placeholder="单笔下限" style="font-size: 26upx;width:220upx;text-align: center;color:#DA53A2;font-weight: bold;">
							</view>
							<view style="width:40upx;height: 3upx;background: rgba(255,255,255,0.2);"></view>
							<view class="right-item" style="height:48upx;">
								<input type="text" placeholder="单笔上限" style="font-size: 26upx;width:220upx;text-align: center;color:#DA53A2;font-weight: bold;" value="10000" disabled>
							</view>
							<view style="width:100%;height:2upx;background: rgba(255,255,255,0.2);margin:10upx 0upx;"></view>
							<view class="left-item" style="padding-top:20upx;">
								<text style="font-size: 24upx;color:#999;">余额100USDT，合计667.58CNY</text>
							</view>
						</view>
					</view>
				</view>
				<view class="fun-card">
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item"><text class="left-item-name">留言</text></view>
							<view class="right-item" style="height:48upx;">
								<text style="font-size: 24upx;color:#999;">1.付款需要些时间，请耐心等待…</text>
								<image :src="imageLib.more"></image>
							</view>
						</view>
					</view>
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
					checked:'../../static/icons/checked.png',
					more:'../../static/icons/more.png'
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
	.radio-box{
		border-radius: 10upx;
		overflow: hidden;
		margin:0px;
		text{
			border-radius: 0px;
		}
	}
	.fun-card-item{
		padding:30upx 40upx;
	}
	.horizon-list-item{
		padding:15upx 0upx;
		display:flex;
		justify-content:space-between;
		align-items:center;
		flex-wrap:wrap;
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
			color:#fff;
			font-size: 26upx;
			image{
				width:36upx;
				height:36upx;
				margin-left:10upx;
			}
		}
	}
	
</style>
