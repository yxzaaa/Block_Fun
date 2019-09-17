<template>
	<view>
		
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="确认订单"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<!-- 新建收货地址 -->
		<navigator class="tosite" url="../choose-address/choose-address" v-if="hasDefault">
			<view class="site">
				<image src="../../static/bg/location.png" style="width:64upx;height:64upx;"></image>
				<span class="person-info">
					<span class="name-phone">
						<span class="name" style="font-size:28upx;color:#fff;">{{addressData.truename}}</span>
						<span class="phone" style="font-size:24upx;color:#999999;">{{addressData.mobile}}</span>
					</span>
					<span class="adress" style="font-size:24upx;display: block;color:#999999;width:500upx;">{{addressData.full}}</span>
				</span>
			</view>
			<image src="../../static/bg/right.png" style="width:40upx;height:40upx;"></image>
		</navigator>
		<navigator url="../address/addressManage" v-else>
			<view class="address">
				<view class="site">
					<image src="../../static/bg/location.png" style="width:64upx;height:64upx;"></image>
					<view class="toaddress" url="../address/addressManage">新建收货地址</view>
				</view>		
				<image src="../../static/bg/right.png" style="width:40upx;height:40upx;"></image>	
			</view>
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
						<span style="font-size: 28upx;color:#fff;">{{item.title.substring(0,36)+' ...'}}</span>
						<text style="font-size:24upx;color:#999999;margin-top:8upx;">{{item.consume}} {{item.amount}}</text>
						<span style="color:#DA53A2;position:relative;">
							<span style="font-size:24upx;margin-right:8upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.symbol}}</span>
							<span style="display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[0]}}</span>
							<span style="font-size:24upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
							<span class="cut" style="position:absolute;right:10upx;bottom:8upx;display: inline-block;">
								<span style="margin-right:20upx;font-size:30upx;color:#fff;font-weight: bold;display: inline-block;"> - </span>
								<span style="display:inline-block;#99999;background:#280617;font-size:24upx;color:#fff;width:64upx;height:40upx;line-height: 40upx;text-align: center;">{{item.number}}</span>
								<span style="margin-left:20upx;font-size:30upx;color:#fff;font-weight: bold;display: inline-block;"> + </span>
							</span>
						</span>
					</view>
				</view>
			</view>
		</view>
		<view class="fixed-buttons">
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
					<fun-button value="提交订单" large wsssidth="240upx" url="../order-management/order-management"></fun-button>
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
				hasDefault:false,
				addressData:{},
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
		onLoad(option){
			//获取当前订单信息
			var item = [{}];
			item[0][option.code] = option.num;
			console.log(item);
			this.$http({
				url:'/mall/buy',
				type:'application/x-www-form-urlencoded',
				data:{
					item:JSON.stringify(item)
				},
				success:res=>{
					console.log(res);
					if(res.code == 200){
						if(res.data.address.length>0){
							this.hasDefault = true;
							this.addressData = res.data.address[0];
							this.addressData.full = res.data.address[0].address;
						}
						//设置订单商品信息
						this.guessList = res.data.mall[0].item;
					}else{
						
					}
				}
			})
		},
		onShow(){
			if(uni.getStorageSync('currAddress')){
				this.addressData = uni.getStorageSync('currAddress');
				uni.removeStorageSync('currAddress');
			}
		},
		methods:{
			
		}
		
	}
</script>

<style lang="scss" scoped>
	.tosite{
		width:750upx;
		height:140upx;
		padding:40upx;
		margin-top:186upx;
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
				.name-phone{
					display: flex;
					align-items: center;
				}
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
	.address{
		width:750upx;
		padding:40upx;
		margin-top:186upx;
		height:140upx;
		border-bottom:1px solid rgba(255,255,255,0.1);
		display:flex;
		align-items:center;
		justify-content:space-between;
		.site{
			display: flex;
			align-items: center;
			.toaddress{
				color:#fff;
				font-size:28upx;
				margin-left:16upx;
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
	.fixed-buttons{
		display: flex;
		justify-content: flex-end;
		align-items: center;
	}
	.button-group{
		width:500upx;
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
