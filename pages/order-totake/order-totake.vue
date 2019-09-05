<template>
	<view>
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="订单详情"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		
		<!-- 待付款计时器 -->
		<view class="topay">
			<view style="display: flex;flex-direction: column;">
				<span style="font-family: PingFang SC;color:#fff;font-size: 32upx;">待收货</span>
				<span style="font-family: PingFang SC;color:#999999;font-size: 24upx;margin-top:12upx;">
					商品已送达
				</span>
			</view>
			<view style="width:105upx;height:78upx;">
				<image src="../../static/bg/take.png" style="width:105upx;height:78upx;display: block;"></image>
			</view>
		</view>
		
		<!-- 收货地址 -->
		<view class="tosite">
			<view class="site">
				<image src="../../static/bg/location.png" style="width:64upx;height:64upx;"></image>
				<span class="person-info">
					<span class="name-phone">
						<span class="name" style="font-size:28upx;color:#fff;">王依依</span>
						<span class="phone" style="font-size:24upx;color:#999999;;">133xxxx1232</span>
					</span>
					<span class="adress" style="font-size:24upx;display: block;color:#999999;;">北京市朝阳区朝阳路朝阳小区10号楼102</span>
				</span>
			</view>
		</view>
		<view class="goodslist">
			<view class="goods"
			v-for="(item,index) in imgList"
			:key = "index"
			>
				<view class="image">
					<image :src="item.image" style="width:160upx;height:160upx;display: block;"></image>
				</view>
				<view class="text">
					<span style="color:#fff;font-size:24upx;font-family: PingFang SC;width:470upx;height:66upx;line-height: 34upx;display: block;">{{item.title}}</span>
					<span style="display: block;">
						<span style="color: #999999;font-size:20upx;margin-right:20upx;">数量：{{item.number}}</span>
						<span style="color: #999999;font-size:20upx;">颜色：{{item.color}}</span>
					</span>
					<span>
						<span style="color:#fff;font-size:28upx;font-family: Montserrat-Bold;margin-right: 6upx;">{{item.symbol}}</span>
						<span style="color:#fff;font-size:28upx;font-weight: bold;font-family: Montserrat-Bold;">{{item.price}}</span>
					</span>
				</view>
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
		<view class="money">
			<span style="color:#fff;font-size: 28upx;margin-right: 20upx;">实付款</span>
			<span style="color:#DA53A2;font-size:28upx;font-family: Montserrat-Bold;font-weight: 600;">￥ 6444.13</span>
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
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},
				},
				imgList:[
					{
						id:1,
						title:'Apple iPhone X (A1865) 256GB 深空灰色 移动联通电信4G手机',
						number:'1',
						color:'白色',
						symbol:'￥',
						price:'6444.12',
						image:"../../static/bg/iphonex.png"
					},
					{
						id:2,
						title:'华为P30 (A1865) 256GB 深空灰色 移动联通电信4G手机',
						number:'1',
						color:'白色',
						symbol:'积分',
						price:'4000',
						image:"../../static/bg/p30.png"
					},
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss" scoped>
	.topay{
		display: flex;
		width:100%;
		height:200upx;
		padding:6upx 40upx 58upx 80upx;
		margin-top:176upx;
		align-items: flex-end;
		justify-content: space-between;
		border-bottom:1px solid rgba(255,255,255,0.1)
	}
	.tosite{
		width:750upx;
		height:64upx;
		padding:40upx;
		padding-top:60upx;
		padding-bottom:80upx;
		border-bottom:1px solid rgba(255,255,255,0.1);
		display:flex;
		align-items:center;
		justify-content:space-between;
		.tosite{
			display: flex;
		}
		.site{
			width:686upx;
			height:106upx;
			display: flex;
			align-items: center;
			.person-info{
				margin-left:20upx;
				.phone{
					margin-left:20upx;
				}
			}
			.toaddress{
				color:#fff;
				font-size:28upx;
				margin-left:32upx;
			}
		}
		
	}
	.goodslist{
		width:100%;
		display: flex;
		flex-direction: column;
		padding:40upx 40upx 0;
		.goods{
			display: flex;
			margin-bottom:40upx;
			.image{
				width:160upx;
				height:160upx;
				margin-right: 20upx;
			}
		}
	}
	.orderinfo{
		width:670upx;
		height:228upx;
		background:#2D1F25;
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
	.money{
		width:100%;
		padding:40upx 40upx 0;
		display: flex;
		justify-content: flex-end;
		align-items: center;;
	}
</style>
