<template>
	<view class="container">
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="支付结果"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view style="width:750upx;height:200upx;margin-top:176upx;text-align: center;">
			<image src="../../static/bg/pays.png" style="width:280upx;height:104upx;"></image>
			<span style="display: block;font-size: 28upx;color:#fff;">支付成功</span>
		</view>
		<hr style="margin-top:40upx;border-bottom:none;background:#fff;opacity: 0.1;"/>
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
		<view class="orderinfo">
			<view class="numinfo">
				<span class="content">订单编号</span>
				<span class="ordernum">123123123</span>
			</view>
			<view class="timeinfo">
				<span class="content">下单时间</span>
				<span class="date">2019-2-2</span>
			</view>
			<view class="paystyle">
				<span class="content">支付方式</span>
				<span class="paynow">现金支付</span>
			</view>
		</view>
		<view class="fixed-buttons">
			<view class="button-group">
				<fun-button value="现金支付" width="670upx" large url="../pay-result/pay-result"></fun-button>
			</view>
		</view>	</view>
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
		padding:80upx 243upx 0;
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
	.orderinfo{
		width:670upx;
		background:#2D1F25;
		margin-top:148upx;
		margin-left:40upx;
		padding:40upx;
		display: flex;
		flex-direction: column;
		align-content:start;
		.numinfo{
			display: flex;
			justify-content: space-between;
			.content{
				font-family: PingFang SC;
				font-size: 24upx;
				color:#fff;
				opacity: 0.5;
			}
			.ordernum{
				font-family: PingFang SC;
				font-size: 24upx;
				color:#fff;
			}
		}
		.timeinfo{
			margin-top:36upx; 
			display: flex;
			justify-content: space-between;
			.content{
				font-family: PingFang SC;
				font-size: 24upx;
				color:#fff;
				opacity: 0.5;
			}
			.date{
				font-family: PingFang SC;
				font-size: 24upx;
				color:#fff;
			}
			
		}
		.paystyle{
			margin-top:36upx;
			display: flex;
			justify-content: space-between;
			.content{
				font-family: PingFang SC;
				font-size: 24upx;
				color:#fff;
				opacity: 0.5;
			}
			.paynow{
				font-family: PingFang SC;
				font-size: 24upx;
				color:#fff;
			}
			
		}
	}

	.button-group{
		width:670upx;
	}
</style>