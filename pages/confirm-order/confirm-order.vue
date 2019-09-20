<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			title="确认订单" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container">
			<navigator class="tosite" url="../choose-address/choose-address">
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
				<image src="../../static/bg/right.png" style="width:40upx;height:40upx;"></image>
			</navigator>
			<!-- 购物车详情 -->
			<view class="guess">
				<view class="guess-list">
					<view 
						v-for="(item, index) in guessList" 
						:key="index"
						class="guess-item"	
					>
					<!-- 引入图片 -->
						<view class="image-wrapper">
							<image 
								:src="item.src" 
								mode="aspectFill"
								style="width:160upx;height:160upx;"
							></image>
						</view>
						<!-- 图片描述 -->
						<view class="guess-content" style="margin-left:20upx;margin-top:0;">
							<span style="font-size: 28upx;color:#fff;">{{item.title}}</span>
							<text style="font-size:24upx;color:#999999;margin-top:12upx;">{{item.consume}} {{item.amount}}</text>
							<span style="color:#DA53A2;position:relative;">
								<span style="font-size:24upx;margin-right:8upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.symbol}}</span>
								<span style="display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[0]}}</span>
								<span style="font-size:24upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
								<span class="cut" style="position:absolute;right:50upx;bottom:4upx;display: inline-block;">
									<span style="margin-right:20upx;font-size:30upx;color:#fff;font-weight: bold;display: inline-block;"> - </span>
									<span style="display:inline-block;#99999;background:#280617;font-size:24upx;color:#fff;width:64upx;height:40upx;line-height: 40upx;text-align: center;">{{item.number}}</span>
									<span style="margin-left:20upx;font-size:30upx;color:#fff;font-weight: bold;display: inline-block;"> + </span>
								</span>
							</span>
						</view>
					</view>
				</view>
			</view>
			<view class="button-group">
				<view class="finish">
					<view class="price">
						<span class="cash">
							<span style="font-size: 24upx;color:#999999">现金：</span>
							<span style="font-size: 24upx;color:#DA53A2;font-family:'Montserrat-Bold';">￥</span>
							<span style="font-size: 28upx;color:#DA53A2;font-family:'Montserrat-Bold';">6444.</span>
							<span style="font-size: 24upx;color:#DA53A2;font-family:'Montserrat-Bold';">12</span>
						</span>
						<span>
							<span style="font-size: 24upx;color:#999999;">积分：</span>
							<span style="font-size: 24upx;color:#fff;">4000</span>
						</span>
					</view>
					<fun-button value="提交订单" width="240upx" url="../pay-order/pay-order"></fun-button>
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
					},
					
				},
				guessList: [{
						src: '../../static/bg/iphonex.png',
						src1:'../../static/bg/checkbox.png',
						title: 'Apple iPhone X (A1865) 256GB 深空灰色 移动联通电信4G手机',
						consume:'消耗积分',
						amount:'4000',
						symbol:"￥",
						price:'6444.13',
						number:'0'
					},
					{
						src: '../../static/bg/p30.png',
						src1:'../../static/bg/check.png',
						title: '华为P30 (A1865) 256GB 深空灰色 移动联通电信4G手机',
						consume:'消耗积分',
						amount:'4000',
						symbol:"￥",
						price:'4999.21',
						number:'0',
					},
					{
						src: '../../static/bg/apple.png',
						src1:'../../static/bg/checkbox.png',
						title: 'Apple iPhone X(A1865) 256GB 深空灰色 移动联通电信4G手机',
						consume:'消耗积分',
						amount:'4000',
						symbol:"￥",
						price:'4999.21',
						number:'0',
					},
				],
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			
		}
	}
</script>

<style lang="scss" scoped>
		.tosite{
			width:750upx;
			height:64upx;
			padding:40upx;
			padding-top:214upx;
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
		.guess {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items:center;
			padding:30upx 40upx 10upx;
		}
		.guess-list {
			margin:0 auto;
			// display: flex;
			// flex-wrap: wrap;
			width:670upx;
		}
		.guess-item {
			display: flex;
			width:100%;
			padding-bottom: 40upx;
		
			.image-wrapper{
				width: 160upx;
				height: 160upx;
				border-radius: 10upx;
			}
			.guess-content{
				height:160upx;
				span,text{
					display: block;
				}
			}
		}
	.button-group{
		width:750upx;
		height:120upx;
		position:fixed;
		bottom:0;
		background:#2F282B;
		padding:20upx 40upx;
		display:flex;
		justify-content:flex-end;
		
		.finish{
			display: flex;
			align-items: center;
			.price{
				display: flex;
				margin-right:20upx;
				flex-direction: column;
				align-content: center;
				align-items: flex-end;
				span{
					display: inline-block;
					line-height:32upx;
				}
			}
		}
	}
	

</style>
