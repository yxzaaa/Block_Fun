<template>
	<view>
		
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="支付订单"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view
			class="payNumber"
			v-for="(item,index) in paynumber"
			:key="index"
		>
			<view class="symbolNumber">
				<span class="symbol">{{item.symbol}}</span>
				<span class="price">{{item.price}}</span>
			</view>
		</view>
		<view class="payStyle">
			<view class="cash">
				<span class="content">
					现金支付
				</span>
				<span class="number"
						v-for="(item,index) in paynumber"
						:key="index"
						>
					<span>
						{{item.symbol}} {{item.price}}
					</span>
					<image src="../../static/bg/check.png" style="width:32upx;height:32upx;margin-left:16upx;"></image>
				</span>
			</view>
			<view class="integral">
				<span class="content">
					积分支付
				</span>
				<span class="number">
					<span style="font-size:28upx;color:#C7C7C7">
						4000
					</span>
					<image src="../../static/bg/checkbox.png" style="width:32upx;height:32upx;margin-left:16upx;"></image>
				</span>
			</view>
		</view>
		<fun-button value="现金支付" width="670upx" class="funbtn" url="../pay-result/pay-result"></fun-button>
	</view>
</template>

<script>
	import FunButton from '@/components/fun-button.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			FunButton,
		},
		data() {
			return {
				scroll:0,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},
				},				
				paynumber:[
					{
						symbol:'￥',
						price:'8398.58',
					}
				],
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
	.payNumber{
		width:750upx;
		height:68upx;
		padding:236upx 243upx 0;
		.symbolNumber{
			width:264upx;
			height:68upx;
		}
		.symbol{
			font-size:28upx;
			font-family:'Montserrat-Bold';
			color:#DA53A2;
			font-weight: 600;
			margin-right:10upx;
		}
		.price{
			font-size:56upx;
			font-family:'Montserrat-Bold';
			color:#DA53A2;
			font-weight: 600;
		}
	}
	.payStyle{
		width:670upx;
		height:228upx;
		background:#2D1F25;
		margin-top:148upx;
		margin-left:40upx;
		padding:40upx;
		display: flex;
		flex-direction: column;
		align-content:start;
		.cash{
			display: flex;
			justify-content: space-between;
			
		}
		.number{
			
			display: flex;
			align-items: center;
			span{
				font-size:28upx;
				color:#DA53A2;
				font-weight:bold;
				font-family:'Montserrat-Bold';
			}
		}
		.integral{
			display: flex;
			justify-content: space-between;
			margin-top:50upx;
		}
		.content{
			color:#fff;
			font-size: 28upx;
		}
	}
	.funbtn{
		position:fixed;
		left:40upx;
		bottom:86upx;
	}
</style>
