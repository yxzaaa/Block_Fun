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
		<view class="app-container full">
			<view 
				style="width:750upx;height:200upx;text-align: center;border-bottom:2upx solid rgba(255,255,255,0.2)"
				v-if="payStatus !== '1'"
			>
				<image src="../../static/bg/pays.png" style="width:280upx;height:104upx;position:relative;left:-8upx;"></image>
				<span style="display: block;font-size: 28upx;color:#fff;line-height: 48upx;">支付成功</span>
			</view>
			<view 
				style="width:750upx;height:200upx;text-align: center;border-bottom:2upx solid rgba(255,255,255,0.2)"
				v-if="payStatus === '1'"
			>
				<image src="../../static/bg/img_right.png" style="width:280upx;height:104upx;position:relative;left:-8upx;"></image>
				<span style="display: block;font-size: 28upx;color:#fff;line-height: 48upx;">支付失败</span>
			</view>
			<view
				class="payNumber"
				v-for="(item,index) in paynumber"
				:key="index"
			>
				<view class="symbolNumber">
					<span class="symbol">￥</span>
					<span class="price">{{amount}}</span>
				</view>
			</view>
			<view class="orderinfo">
				<view class="numinfo">
					<span class="content">订单编号</span>
					<span class="ordernum">{{orderId}}</span>
				</view>
				<view class="timeinfo">
					<span class="content">下单时间</span>
					<span class="date">{{createTime}}</span>
				</view>
				<view class="paystyle">
					<span class="content">支付方式</span>
					<span class="paynow">{{payment}}</span>
				</view>
			</view>
			<view class="fixed-buttons">
				<view class="button-group" style="width:670upx;">
					<fun-button type="light" value="返回首页" width="320upx" large @handle="backHome"></fun-button>
					<fun-button v-if="payStatus !== '1'" value="订单详情" width="320upx" large @handle="orderDetail"></fun-button>
					<fun-button v-if="payStatus === '1'" value="重新支付" width="320upx" large @handle="rePay"></fun-button>
				</view>
			</view>
		</view>
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
				orderId:null,
				payStatus:'1',
				createTime:'',
				payment:'',
				amount:'',
			}
		},
		onLoad(option){
			this.orderId = option.id;
			//根据订单id获取订单详情，判断支付结果
			this.$http({
				url:'/order/show?id='+this.orderId,
				success:res=>{
					console.log(res);
					if(res.code == 200){
						this.payStatus = res.data.status;
						this.createTime = res.data.create;
						this.payment = res.data.payment;
						this.amount = res.data.amount;
					}
				}
			})
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods: {
			backHome(){
				uni.reLaunch({
					url:'../shopping/shopping'
				})
			},
			orderDetail(){
				uni.navigateTo({
					url:'../order-dealing/order-dealing?id='+this.orderId
				})
			},
			rePay(){
				uni.navigateBack({
					delta:1
				})
			}
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
			font-size:32upx;
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
		border-radius: 8upx;
		overflow: hidden;
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