<template>
	<view class="container">
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="订单详情"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full">
			<!-- 待付款计时器 -->
			<view class="topay" v-if="!loading">
				<view style="display: flex;flex-direction: column;">
					<span style="color:#fff;font-size: 32upx;">{{getStatus(orderInfo.status).status}}</span>
					<span style="color:#999999;font-size: 24upx;margin-top:12upx;" v-if="orderInfo.status == 1">
						订单将于<span style="color:#DA53A2;padding:0px 6upx;display: inline-block;">{{getOrderDelay()}}</span>后关闭
					</span>
					<span style="color:#999999;font-size: 24upx;margin-top:12upx;" v-else>
						{{getContent(orderInfo.status)}}
					</span>
				</view>
				<view style="width:218upx;height:136upx;position: relative;top:-20upx;">
					<image :src="getStatus(orderInfo.status).img" style="width:218upx;height:136upx;display: block;"></image>
				</view>
			</view>
			
			<!-- 收货地址 -->
			<view class="tosite" v-if="!loading">
				<view class="site">
					<view>
						<image src="../../static/bg/location.png" style="width:64upx;height:64upx;"></image>
					</view>
					<span class="person-info">
						<span class="name-phone">
							<span class="name" style="font-size:28upx;color:#fff;">{{orderInfo.truename}}</span>
							<span class="phone" style="font-size:24upx;color:#999999;;">{{orderInfo.mobile}}</span>
						</span>
						<span class="adress" style="font-size:24upx;display: block;color:#999999;;">{{orderInfo.address}}</span>
					</span>
				</view>
			</view>
			<view class="goodslist" v-if="!loading">
				<view class="goods"
				v-for="(item,index) in orderInfo.item"
				:key = "index"
				>
					<view class="image">
						<image :src="item.img" style="width:160upx;height:160upx;display: block;"></image>
					</view>
					<view class="text">
						<span style="color:#fff;font-size:24upx;width:470upx;height:66upx;line-height: 34upx;display: block;">{{item.title.length>36?item.title.substring(0,36)+' ...':item.title}}</span>
						<span style="display: block;">
							<span style="color: #999999;font-size:20upx;margin-right:20upx;">数量：{{item.number}}</span>
							<span style="color: #999999;font-size:20upx;margin-right:20upx;">{{item.p1}}：{{item.s1}}</span>
							<span style="color: #999999;font-size:20upx;" v-if="item.p2">{{item.p2}}：{{item.s2}}</span>
						</span>
						
						<span>
							<span style="color:#fff;font-size:28upx;font-family: Montserrat-Bold;margin-right: 6upx;">￥</span>
							<span style="color:#fff;font-size:28upx;font-weight: bold;font-family: Montserrat-Bold;">{{item.price}}</span>
						</span>
					</view>
				</view>
			</view>
			<view class="orderinfo" v-if="!loading">
				<view class="numinfo">
					<span class="content">订单编号</span>
					<span class="ordernum">{{orderInfo.id}}</span>
				</view>
				<view class="timeinfo">
					<span class="content">下单时间</span>
					<span class="date">{{orderInfo.create}}</span>
				</view>
				<view class="paystyle">
					<span class="content">支付方式</span>
					<span class="paynow">{{orderInfo.payment}}</span>
				</view>
			</view>
			<view class="money" v-if="!loading">
				<span style="color:#fff;font-size: 28upx;margin-right: 20upx;">实付款</span>
				<span style="color:#DA53A2;font-size:28upx;font-family: Montserrat-Bold;font-weight: 600;">￥ {{orderInfo.amount}}</span>
			</view>
			<view style="padding:10upx 40upx;" v-if="loading">
				<Skeleton height="200upx" :loading="loading"></Skeleton>
				<Skeleton height="140upx" :loading="loading"></Skeleton>
				<Skeleton height="200upx" :loading="loading"></Skeleton>
				<Skeleton height="250upx" :loading="loading"></Skeleton>
				<Skeleton height="48upx" width="120upx" :loading="loading"></Skeleton>
			</view>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import Skeleton from '@/components/Skeleton.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			Skeleton
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
				getDelay:0,
				timer:null,
				orderInfo:{},
				loading:true
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(option){
			this.orderId = option.id;
			//根据订单id获取订单详情，判断支付结果
			this.getOrderDetail();
		},
		methods: {
			getOrderDetail(){
				this.$http({
					url:'/order/show?id='+this.orderId,
					success:res=>{
						console.log(res);
						if(res.code == 200){
							this.orderInfo = res.data;
							this.getDelay = res.data.limit;
							this.loading = false;
							if(this.getDelay > 0){
								this.timer = setInterval(()=>{
									this.getDelay --;
									if(this.getDelay == 0){
										this.getOrderDetail();
										clearInterval(this.timer);
										this.timer = null;
									}
								},1000);
							}
						}
					}
				})
			},
			getOrderDelay(){
				var hh = 0,mm = 0,ss = 0;
				hh = Math.floor(this.getDelay/3600);
				mm = Math.floor((this.getDelay - hh*3600)/60);
				ss = this.getDelay - hh*3600 - mm*60;
				hh = hh>=10?hh:'0'+hh;
				mm = mm>=10?mm:'0'+mm;
				ss = ss>=10?ss:'0'+ss;
				if(hh == 0){
					return mm+'分'+ss+'秒';
				}else if(hh == 0 && mm == 0){
					return ss+'秒';
				}else{
					return hh+'时'+mm+'分'+ss+'秒';
				}
				
			},
			getStatus(status){
				var currStatus = '',currImg='';
				switch(status){
					case 1:
						currStatus = '待付款';
						currImg = '../../static/bg/orders/img_time.png';
						break;
					case 2:
						currStatus = '待发货';
						currImg = '../../static/bg/orders/img_rong.png';
						break;
					case 3:
						currStatus = '待收货';
						currImg = '../../static/bg/orders/img_truck.png';
						break;
					case 4:
						currStatus = '已完成';
						currImg = '../../static/bg/orders/img_finish.png';
						break;
					case 8:
						currStatus = '已取消';
						currImg = '../../static/bg/orders/img_right.png';
						break;
				}
				return {
					status:currStatus,
					img:currImg
				};
			},
			getContent(status){
				var currContent="";
				switch(status){
					case 2:
						currContent = '等待发货';
						break;
					case 3:
						if(this.orderInfo.receive !== ''){
							currContent = '商品已送达';
						}else{
							currContent = '物流运输中';
						}
						break;
					case 4:
						currContent = '您已确认收货';
						break;
					case 8:
						currContent = '订单已取消';
						break;
				}
				return currContent;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.topay{
		display: flex;
		width:100%;
		height:200upx;
		padding:0px 40upx;
		padding-left:80upx;
		align-items: center;
		justify-content: space-between;
		border-bottom:1px solid rgba(255,255,255,0.1);
	}
	.tosite{
		width:750upx;
		padding:28upx 40upx;
		border-bottom:1px solid rgba(255,255,255,0.1);
		display:flex;
		align-items:center;
		justify-content:flex-start;
		.site{
			width:686upx;
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
				overflow: hidden;
				border-radius: 8upx;
			}
		}
	}
	.orderinfo{
		width:670upx;
		background:#2D1F25;
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
				font-size: 24upx;
				color:#fff;
				opacity: 0.5;
			}
			.ordernum{
				font-size: 24upx;
				color:#fff;
			}
		}
		.timeinfo{
			margin-top:36upx; 
			display: flex;
			justify-content: space-between;
			.content{
				font-size: 24upx;
				color:#fff;
				opacity: 0.5;
			}
			.date{
				font-size: 24upx;
				color:#fff;
			}	
		}
		.paystyle{
			margin-top:36upx;
			display: flex;
			justify-content: space-between;
			.content{
				font-size: 24upx;
				color:#fff;
				opacity: 0.5;
			}
			.paynow{
				font-size: 24upx;
				color:#fff;
			}
			
		}
	}
	.money{
		width:100%;
		padding:40upx;
		padding-bottom:80upx;
		display: flex;
		justify-content: flex-end;
		align-items: center;;
	}
</style>
