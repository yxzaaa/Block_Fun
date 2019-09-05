<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="购买会员" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full fixbutton">
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button 
						value="立即购买" 
						width="670upx" 
						type="light" 
						large 
						color="#26262B"
						background="#B69B6F"
						icon="../../static/icons/icon_buy.png"
						@handle="openVip()"
					></fun-button>
				</view>
			</view>
			<view style="padding:0upx 40upx;padding-bottom:30upx;">
				<view class="fun-card" style="background:#B69B6F;border-radius: 24upx;">
					<image :src="imageLib.cardbg" class="card-bg"></image>
					<view class="fun-card-item" style="padding-top:26upx;padding-bottom:26upx;position: relative;z-index:1;">
						<view class="main-title gold" style="display: flex;justify-content: center;align-items: center;">
							<image :src="imageLib.vip" style="width:40upx;height:40upx;margin-right:16upx;"></image>
							会员权益说明
						</view>
						<view class="section-content" style="padding:5upx 0upx;">
							<text class="section-describe">
								1.享受钱包手续费分红（总收益的30%），按照每位用户的锁仓比例，进行分红;
							</text>
							<text class="section-describe">
								1.自主锁仓资格；
							</text>
							<text class="section-describe">
								1.OTC挂单资格；
							</text>
							<text class="section-describe">
								1.金牌理财资格（私募）。
							</text>
						</view>
					</view>
				</view>
				<view class="section-content" style="padding:40upx 0upx;">
					<view class="section-subtitle" style="color:#CCB382;">规则说明</view>
					<view class="section-part">
						<span class="list-num">1.</span> 
						会员费用为199USDT/年，自付费之日起，到下一年的今日此时失效。如会员到期，可自行选择是否继续购买。
					</view>
					<view class="section-part">
						<span class="list-num">2.</span>
						支付的费用将从您的USDT钱包账户中直接扣除，请保证余额充足。
					</view>
					<view class="section-part">
						<span class="list-num">3.</span>
						会员费用一旦支付，不可退还，还望悉知。
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
					vip:'../../static/icons/icon_vip.png',
					cardbg:'../../static/bg4.jpg'
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
	.main-title{
		font-size:36upx;
		color:#fff;
		text-align: center;
		line-height: 64upx;
		font-weight:bolder;
		padding-bottom:10upx;
		&.gold{
			color:#26262B;
		}
	}
	.card-bg{
		position: absolute;
		top:0px;
		left:0px;
		width:100%;
		height:100%;
		z-index:0;
	}
	.gold-button{
		width:100%;
		border-radius: 10upx;
		line-height: 80upx;
		position:relative;
		overflow:hidden;
		margin-top:20upx;
		text-align:center;
		image{
			position:absolute;
			top:0px;
			left:0px;
			width:100%;
			height:100%;
			z-index:0;
		}
		text{
			font-weight: bold;
		}
	}
	.section-part{
		position: relative;
		padding-left:30upx;
		.list-num{
			position: absolute;
			line-height: 30upx;
			top:12upx;
			left:0upx;
		}
	}
	.section-describe{
		display: block;
		color:#26262B;
	}
	.section-part{
		color:#CCB382;
	}
	
</style>
