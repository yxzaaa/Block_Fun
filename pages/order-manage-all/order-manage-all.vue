<template>
	<view class="container">
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
			<view class="managebox" v-for="(val,index) in orderList" :key="index"> <!-- 待办管理 -->
				<view class="backlog"> 
					<span>{{val.id}}</span>
					<view :style="{fontSize: '28upx',color:getStatus(val.status).color }">{{getStatus(val.status).name}}</view>
				</view>
				<view class="goodslist">
					<view class="goods" v-for="val1 in val.item">
						<view class="image">
							<image :src="val1.img" style="width:160upx;height:160upx;display: block;"></image>
						</view>
						<view class="text">
							<span style="color:#fff;font-size:24upx;width:470upx;height:66upx;line-height: 34upx;display: block;">{{val1.title}}</span>
							<span style="display: block;">
								<span style="color: #999999;font-size:24upx;margin-right:24upx;">数量：{{val1.number}}</span>
								<span style="color: #999999;font-size:24upx;">{{val1.p1}}：{{val1.s1}}</span>
								<span style="color: #999999;font-size:24upx;margin-left:24upx;" v-if="val1.p2">{{val1.p2}}：{{val1.s2}}</span>
							</span>
							<span>
								<span style="color:#fff;font-size:28upx;font-family: Montserrat-Bold;margin-right: 6upx;">￥</span>
								<span style="color:#fff;font-size:28upx;font-weight: bold;font-family: Montserrat-Bold;">{{val1.price}}</span>
							</span>
						</view>
					</view>
				</view>
				<view class="account">
					<span style="color:#fff;font-size: 24upx;opacity: 0.7;margin-right:24upx;">
						共 <span style="margin:0 6upx;"> {{getTotalNum(val.item)}} </span> 件
					</span>
					<span style="color:#fff;font-size: 28upx;">
						合计<span style="color:#DA53A2;font-family: Montserrat-Bold;font-weight: 600;margin-left:12upx;">￥{{val.amount}}</span>
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
					{id:-1,text:'全部',color:''},
					{id:1,text:'待付款',color:'#DA53A2'},
					{id:2,text:'处理中',color:'#F2C94C'},
					{id:3,text:'待收货',color:'#56CCF2'},
					{id:4,text:'已完成',color:'#999999'},
					{id:8,text:'买家关闭订单',color:'#999999'},
					{id:9,text:'卖家关闭订单',color:'#999999'},
				],
				orderList:[],
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
			this.toggleStatus(0);
		},
		methods: {
			toggleStatus(index){
				console.log(this.statusTabs[index].id);
				this.$http({
					url:'/member/order?nav='+this.statusTabs[index].id+'&page=1',
					success:res=>{
						this.orderList = res.data.item;
						console.log(this.orderList);
					}
				})
			},
			getStatus(id){
				console.log(id);
				var name = '',color = '';
				this.statusTabs.map(item=>{
					if(item.id == id){
						name = item.text;
						color = item.color;
					}
				})
				return {
					name,
					color
				};
			},
			getTotalNum(item){
				var total = 0;
				item.map(per=>{
					total += per.number
				})
				return total;
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
