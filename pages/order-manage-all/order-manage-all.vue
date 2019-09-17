<template>
	<view>
		<uni-background />
		<uni-nav-bar
			title="订单管理" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full">
			
			<!-- 顶部滑动 -->
			<horizon-tab :tabs="statusTabs" padding="45" @click="toggleStatus" ></horizon-tab>
			
			<view class="managebox"> <!-- 待办管理 -->
				<view class="backlog"> 
					<span>tb31231234234314</span>
					<view style="font-size: 28upx;color: #DA53A2;">待付款</view>
				</view>
				<view class="goodslist">
					<block 
					v-for="(item,index) in imgList"
					:key = "index"
					>
						<navigator class="goods" :url="'../order-topay/order-topay?id='+index">
							<view class="image">
								<image :src="item.image" style="width:160upx;height:160upx;display: block;"></image>
							</view>
							<view class="text">
								<span style="color:#fff;font-size:24upx;width:470upx;height:66upx;line-height: 34upx;display: block;">{{item.title}}</span>
								<span style="display: block;">
									<span style="color: #999999;font-size:24upx;margin-right:24upx;">数量：{{item.number}}</span>
									<span style="color: #999999;font-size:24upx;">颜色：{{item.color}}</span>
								</span>
								<span>
									<span style="color:#fff;font-size:28upx;font-family: Montserrat-Bold;margin-right: 6upx;">{{item.symbol}}</span>
									<span style="color:#fff;font-size:28upx;font-weight: bold;font-family: Montserrat-Bold;">{{item.price}}</span>
								</span>
							</view>
						</navigator>
					</block>
				</view>
				<view class="account">
					<span style="color:#fff;font-size: 24upx;opacity: 0.7;margin-right:24upx;">
						共 <span style="margin:0 6upx;"> 2 </span> 件
					</span>
					<span style="color:#fff;font-size: 28upx;">
						合计<span style="color:#DA53A2;font-family: Montserrat-Bold;font-weight: 600;margin-left:12upx;">￥ 6444.13</span>
					</span>
				</view>
				<view class="button-group">
					<fun-button value="取消订单" width="200upx" class="funbtn1" background="#291A21" color="#999"></fun-button>
					<fun-button value="去支付" width="200upx" class="funbtn" url="../pay-order/pay-order"></fun-button>
				</view>
			</view>
			<view class="managebox"> <!-- 待办管理 -->
				<view class="backlog"> 
					<span>tb31231234234314</span>
					<view style="font-size: 28upx;color: #56CCF2;">待收货</view>
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
							<span style="color:#fff;font-size:24upx;width:470upx;height:66upx;line-height: 34upx;display: block;">{{item.title}}</span>
							<span style="display: block;">
								<span style="color: #999999;font-size:24upx;margin-right:24upx;">数量：{{item.number}}</span>
								<span style="color: #999999;font-size:24upx;">颜色：{{item.color}}</span>
							</span>
							<span>
								<span style="color:#fff;font-size:28upx;font-family: Montserrat-Bold;margin-right: 6upx;">{{item.symbol}}</span>
								<span style="color:#fff;font-size:28upx;font-weight: bold;font-family: Montserrat-Bold;">{{item.price}}</span>
							</span>
						</view>
					</view>
				</view>
				<view class="account">
					<span style="color:#fff;font-size: 24upx;opacity: 0.7;margin-right:24upx;">
						共 <span style="margin:0 6upx;"> 2 </span> 件
					</span>
					<span style="color:#fff;font-size: 28upx;">
						合计<span style="color:#DA53A2;font-family: Montserrat-Bold;font-weight: 600;margin-left:12upx;">￥ 6444.13</span>
					</span>
				</view>
				<view class="button-group">
					<fun-button value="确认收货" width="200upx" class="funbtn"></fun-button>
				</view>
			</view>
			<view class="managebox"> <!-- 待办管理 -->
				<view class="backlog"> 
					<span>tb31231234234314</span>
					<view style="font-size: 28upx;color: #F2C94C;">待处理</view>
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
							<span style="color:#fff;font-size:24upx;width:470upx;height:66upx;line-height: 34upx;display: block;">{{item.title}}</span>
							<span style="display: block;">
								<span style="color: #999999;font-size:24upx;margin-right:24upx;">数量：{{item.number}}</span>
								<span style="color: #999999;font-size:24upx;">颜色：{{item.color}}</span>
							</span>
							<span>
								<span style="color:#fff;font-size:28upx;font-family: Montserrat-Bold;margin-right: 6upx;">{{item.symbol}}</span>
								<span style="color:#fff;font-size:28upx;font-weight: bold;font-family: Montserrat-Bold;">{{item.price}}</span>
							</span>
						</view>
					</view>
				</view>
				<view class="account">
					<span style="color:#fff;font-size: 24upx;opacity: 0.7;margin-right:24upx;">
						共 <span style="margin:0 6upx;"> 2 </span> 件
					</span>
					<span style="color:#fff;font-size: 28upx;">
						合计<span style="color:#DA53A2;font-family: Montserrat-Bold;font-weight: 600;margin-left:12upx;">￥ 6444.13</span>
					</span>
				</view>
				<view class="button-group">
					<fun-button value="取消订单" background="#291A21" color="#999999" width="200upx" class="funbtn"></fun-button>
				</view>
			</view>
			<view class="managebox"> <!-- 待办管理 -->
				<view class="backlog"> 
					<span>tb31231234234314</span>
					<view style="font-size: 28upx;color: #999999;">已取消</view>
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
							<span style="color:#fff;font-size:24upx;width:470upx;height:66upx;line-height: 34upx;display: block;">{{item.title}}</span>
							<span style="display: block;">
								<span style="color: #999999;font-size:24upx;margin-right:24upx;">数量：{{item.number}}</span>
								<span style="color: #999999;font-size:24upx;">颜色：{{item.color}}</span>
							</span>
							<span>
								<span style="color:#fff;font-size:28upx;font-family: Montserrat-Bold;margin-right: 6upx;">{{item.symbol}}</span>
								<span style="color:#fff;font-size:28upx;font-weight: bold;font-family: Montserrat-Bold;">{{item.price}}</span>
							</span>
						</view>
					</view>
				</view>
				<view class="account">
					<span style="color:#fff;font-size: 24upx;opacity: 0.7;margin-right:24upx;">
						共 <span style="margin:0 6upx;"> 2 </span> 件
					</span>
					<span style="color:#fff;font-size: 28upx;">
						合计<span style="color:#DA53A2;font-family: Montserrat-Bold;font-weight: 600;margin-left:12upx;">￥ 6444.13</span>
					</span>
				</view>
			</view>
			<view class="managebox"> <!-- 待办管理 -->
				<view class="backlog"> 
					<span>tb31231234234314</span>
					<view style="font-size: 28upx;color: #999999;">已完成</view>
				</view>
				<view class="goodslist">
					<view class="goods"
					v-for="(item,index) in orderList"
					:key = "index"
					>
						<view class="image">
							<image :src="item.image" style="width:160upx;height:160upx;display: block;"></image>
						</view>
						<view class="text">
							<span style="color:#fff;font-size:24upx;width:470upx;height:66upx;line-height: 34upx;display: block;">{{item.title}}</span>
							<span style="display: block;">
								<span style="color: #999999;font-size:24upx;margin-right:24upx;">数量：{{item.number}}</span>
								<span style="color: #999999;font-size:24upx;">颜色：{{item.color}}</span>
							</span>
							<span>
								<span style="color:#fff;font-size:28upx;font-family: Montserrat-Bold;margin-right: 6upx;">{{item.symbol}}</span>
								<span style="color:#fff;font-size:28upx;font-weight: bold;font-family: Montserrat-Bold;">{{item.price}}</span>
							</span>
						</view>
					</view>
				</view>
				<view class="account">
					<span style="color:#fff;font-size: 24upx;opacity: 0.7;margin-right:24upx;">
						共 <span style="margin:0 6upx;"> 2 </span> 件
					</span>
					<span style="color:#fff;font-size: 28upx;">
						合计<span style="color:#DA53A2;font-family: Montserrat-Bold;font-weight: 600;margin-left:12upx;">￥ 6444.13</span>
					</span>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import HorizonTab from '@/components/horizon-tab.vue';
	import FunButton from '@/components/fun-button.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			HorizonTab,
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
				statusTabs:[
					{id:-1,text:'全部'},
					{id:1,text:'待付款'},
					{id:2,text:'处理中'},
					{id:3,text:'待收货'},
					{id:4,text:'已完成'},
				],
				orderList:[
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
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		// onLoad(){
		// 	this.$http({
		// 		url:'order/show?id',
		// 		success:res=>{
		// 			console.log(res)
		// 		}
		// 	})
		// },
		methods: {
			toggleStatus(index){
				console.log(this.statusTabs[index].id);
				this.$http({
					url:'/member/order?nav='+this.statusTabs[index].id+'&page=1',
					success:res=>{
						console.log(res);
						this.orderList = res.data.item;
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.managebox{
		width:750upx;
		padding:60upx 40upx;
		border-bottom:1px solid rgba(255,255,255,0.1);
		.backlog{
			width:670upx;
			height:40upx;
			display: flex;
			justify-content: space-between;
			align-items:center;
			span{
				font-size: 28upx;
				color:#fff;
			}
		}
		.goodslist{
			width:100%;
			margin:60upx 0 0 0;
			display: flex;
			flex-direction: column;
			flex-shrink:0;
			.goods{
				display: flex;
				margin-bottom:40upx;
				.image{
					width:160upx;
					height:160upx;
					margin-right: 24upx;
				}
			}
		}
		.account{
			display: flex;
			justify-content: flex-end;
			align-items: center;
		}
	}
	.button-group{
		display: flex;
		justify-content:flex-end;
		margin-top:64upx;
		.funbtn1{
			margin-right:40upx;
		}
	}
</style>
