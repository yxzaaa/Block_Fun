<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			title="抵押借贷记录" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full">
			<view class="fix-tabs-box">
				<view class="fix-tabs-item">
					<text :class="{active:activeTab == 2}" @click="toggleTab(2)">我的借款</text>
				</view>
				<view class="fix-tabs-item">
					<text :class="{active:activeTab == 1}" @click="toggleTab(1)">我的投资</text>
				</view>
			</view>
			<scroll-view scroll-y='true' style="width:100%;height:calc(100vh - 274upx);">
				<view class="totalBox">
					<view class="borrow">
						<span class="content">投资总额（USDT）</span>
						<span class="number">{{getNum(investMent)}}</span>
					</view>
					<view class="pledge">
						<span class="content">我的收益（USTD）</span>
						<span class="number">{{getNum(interest)}}</span>
					</view>
				</view>
				<view class="selected">
					<span>订单筛选</span>
					<view class="right-item" style="height:48upx;">
						<picker @change="pickerChange" :value="currClass" :range="classLib" mode="selector" range-key="name">
							<view style="padding:0upx 20upx;font-size:24upx;height:100%;background: #2D1F25;border-radius:8upx;line-height: 48upx;color:#fff;display: flex;justify-content: center;align-items: center;">
								<text style="color:#999;">{{classLib[currClass].name}}</text>
								<image :src="imageLib.sanjiao" style="width:20upx;height:14upx;margin-left:10upx;"></image>
							</view>
						</picker>
					</view>
					</picker>
				</view>
				<view style="padding:40upx;padding-bottom:0px;">
					<block v-for="(item,index) in borrowList" :key="index">
						<view class="debitbox" @click="goPayBack(item)">
							<view class="horizon-list-item">
								<text style="font-size: 28upx;color:#fff;">{{getStatus(item.status)}}</text>
								<text style="color:#DA53A2;">距离还款日还有{{getTimeDelay(item.expired_on)}}天</text>
							</view>
							<view class="order-info">
								<span>{{getDate(item.created_on)}}</span>
								<span>订单号：
									<span>{{item.id}}</span>
								</span>
							</view>
							<view class="debit-info">
								<view class="borrow">
									<span class="content">投资金额（USDT）</span>
									<span class="number">{{getNum(item.total)}}</span>
								</view>
								<view class="pledge">
									<span class="content">到期收益（USDT）</span>
									<span class="number">{{getNum(item.interest)}}</span>
								</view>
							</view>
							<view class="debit-btn">
								<view>
									<span class="content">综合利率</span>
									<span class="number">{{item.rate*100}}%</span>
								</view>
								<view>
									<span class="content">周期</span>
									<span class="number">{{item.month}}月</span>
								</view>
								<view>
									<span class="content">投资结束日</span>
									<span class="number">{{getDate(item.expired_on)}}</span>
								</view>
							</view>
						</view>
					</block>
				</view>
			</scroll-view>
			</swiper>
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
				activeTab:2,
				currPage:1,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},		
				},
				imageLib:{
					sold:'../../static/icons/icon_sold.png',
					bought:'../../static/icons/icon_bought.png',
					alipay:'../../static/icons/icon_alipay.png',
					wechatpay:'../../static/icons/icon_wechatpay.png',
					unionpay:'../../static/icons/icon_unionpay.png',
					sanjiao:'../../static/icons/sanjiao.png',
					add:'../../static/icons/icon_add.png',
				},
				investMent:0,
				interest:0,
				borrowList:[],
				currClass:0,
				classLib:[
					{
						value:0,
						name:'全部'
					},
					{
						value:1,
						name:'进行中'
					},
					{
						value:2,
						name:'已还款'
					},
				],
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onShow(){
			this.updateList();
		},
		methods: {
			updateList(){
				uni.showLoading({
					title:'订单加载中...'
				})
				//获取我的订单列表
				this.$http({
					url:'/v1/main/debit/debit-order-list',
					data:{
						type:this.activeTab,
						status:this.classLib[this.currClass].value,
						page:this.currPage
					},
					success:res=>{
						console.log(res);
						if(res.code == 200){
							uni.hideLoading();
							this.investMent = res.data.investment;
							this.interest = res.data.interest;
							this.borrowList = res.data.item;
						}
					}
				})
			},
			//去还款
			goPayBack(info){
				if(info.status == 1){
					uni.setStorage({
						key:"pay_back_info",
						data:info,
						success:res=>{
							uni.navigateTo({
								url:'../paybackbill/paybackbill'
							})
						}
					})
				}
			},
			getNum(num){
				return (parseFloat(num)).toFixed(2);
			},
			getStatus(status){
				var text = '';
				this.classLib.map(item=>{
					if(item.value == status){
						text = item.name;
					}
				})
				return text;
			},
			getDate(timestamp){
				var date = new Date(timestamp*1000);
				var year = date.getFullYear();
				var month = date.getMonth() + 1;
				var day = date.getDate();
				var hour = date.getHours();
				var min = date.getMinutes();
				month = month>=10?month:'0'+month;
				day = day>=10?day:'0'+day;
				hour = hour>=10?hour:'0'+hour;
				min = min>=10?min:'0'+min;
				return year+'/'+month+'/'+day+' '+hour+':'+min
			},
			getTimeDelay(end){
				var stamp = new Date().getTime();
				var overDay = parseInt((end*1000 - stamp)/(24*3600*1000));
				return overDay;
			},
			tabChange(value){
				this.activeTab = value.detail.current;
			},
			toggleTab(index){
				this.activeTab = index;
				this.updateList();
			},
			publish(){
				uni.navigateTo({
					url:'../publishborrow/publishborrow'
				})
			},
			pickerChange(e){
				console.log(e);
				this.currClass = e.target.value;
				this.updateList();
			}
		}
	}
</script>

<style lang="scss" scoped> 
	.swiper-box{
		height:calc(100vh - 274upx);
	}
	.debitbox{
		width:670upx;
		background: rgba(45, 31, 37,0.8);
		border-radius: 8upx;
		margin-bottom:30upx;
		.horizon-list-item{
			padding:40upx;
			padding-bottom: 0;
			display: flex;
			justify-content: space-between;
			text{
				color:#999;
				font-size: 24upx;
			}
		}
		.debit-info{
			display: flex;
			justify-content: space-between;
			padding:40upx 70upx 50upx;
			border-bottom:1px solid rgba(255,255,255,0.1);
			view{
				display: flex;
				flex-direction: column;
				align-items: center;
				.content{
					font-size: 24upx;
					color:#fff;
					opacity: 0.5;
				}
				.number{
					margin-top:10upx;
					font-size:52upx;
					color:#fff;
					font-weight: 600;
				}
			}
		}
		.debit-btn{
			padding: 30upx 60upx;
			display:flex;
			justify-content:space-between;
			align-items:center;
			view{
				display: flex;
				flex-direction: column;
				align-items: center;
				.content{
					color:#fff;
					opacity: 0.5;
					font-size: 24upx;
				}
				.number{
					color:#fff;
					font-size: 24upx;
					margin-top:20upx;
				}
			}
		}
	}
	.fiexd-btn{
		position: fixed;
		right:70upx;
		bottom:120upx;
		background: #fff;
		width:98upx;
		height:96upx;
		border-radius: 48upx;
		box-shadow: 0px 0px 10px rgba(0, 9, 33, 0.4);
		display:flex;
		justify-content:center;
		align-items:center;
		z-index:998;
		image{
			width:64upx;
			height:64upx;
		}
	}
	.totalBox{
		width:750upx;
		display: flex;
		justify-content: space-between;
		padding:70upx 120upx;
		view{
			display: flex;
			flex-direction: column;
			align-items: center;
			.content{
				font-size: 24upx;
				color:#fff;
				opacity: 0.5;
			}
			.number{
				font-size:52upx;
				color:#fff;
				font-weight: 600;
			}
		}
	}
	.selected{
		display: flex;
		justify-content: space-between;
		align-items: center;
		width:750upx;
		padding:0 40upx;
		span{			
			color: #FFFFFF;
			font-size: 24upx;
			opacity: 0.5;
			margin-top: 10upx;
		}
	}
	.order-info{
		display: flex;
		flex-direction: column;
		padding:16upx 40upx 0upx;
		span{
			color:#999;
			font-size: 24upx;
			margin-bottom: 12upx;
		}
	}
</style>
