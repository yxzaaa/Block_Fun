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
					<text :class="{active:activeTab == 0}" @click="toggleTab(0)">我的借款</text>
				</view>
				<view class="fix-tabs-item">
					<text :class="{active:activeTab == 1}" @click="toggleTab(1)">我的投资</text>
				</view>
			</view>
			<swiper class="swiper-box" :current="activeTab" @change="tabChange">
				<swiper-item>
					<scroll-view scroll-y='true' style="width:100%;height:100%;">
						<view class="totalBox">
							<view class="borrow">
								<span class="content">借款总额（USDT）</span>
								<span class="number">{{debit}}</span>
							</view>
							<view class="pledge">
								<span class="content">抵押总量（Forest）</span>
								<span class="number">{{mortgage}}</span>
							</view>
						</view>
						<view class="selected">
							<span>订单筛选</span>
							<view class="right-item" style="height:48upx;">
								<picker @change="pickerChange" :value="currClass" :range="classLib" mode="selector">
									<view style="padding:0upx 20upx;font-size:24upx;height:100%;background: #2D1F25;line-height: 48upx;color:#fff;display: flex;justify-content: center;align-items: center;">
										<text style="color:#999;">{{classLib[currClass]}}</text>
										<image :src="imageLib.sanjiao" style="width:20upx;height:14upx;"></image>
									</view>
								</picker>
							</view>
							</picker>
						</view>
						<view style="padding:40upx;padding-bottom:0px;">
							<block v-for="(item,index) in borrowList" :key="index">
								<view class="debitbox">
									<view class="horizon-list-item">
										<text style="font-size: 28upx;color:#fff;">{{item.status}}</text>
										<text style="color:#DA53A2;">距离还款日还有10天</text>
									</view>
									<view class="order-info">
										<span>{{item.created_on}}</span>
										<span>订单号：
											<span>{{item.id}}</span>
										</span>
									</view>
									<view class="debit-info">
										<view class="borrow">
											<span class="content">借款总额（USDT）</span>
											<span class="number">{{item.total}}</span>
										</view>
										<view class="pledge">
											<span class="content">抵押总量（Forest）</span>
											<span class="number">{{item.amount}}</span>
										</view>
									</view>
									<view class="debit-btn">
										<view>
											<span class="content">综合利率</span>
											<span class="number">{{item.rate}}</span>
										</view>
										<view>
											<span class="content">周期</span>
											<span class="number">{{item.month}}</span>
										</view>
										<view>
											<span class="content">还款日</span>
											<span class="number">{{item.expired_on}}</span>
										</view>
									</view>
								</view>
							</block>
						</view>
					</scroll-view>
				</swiper-item>
				<swiper-item>
					<scroll-view scroll-y='true' style="width:100%;height:100%;">
						<view class="totalBox">
							<view class="borrow">
								<span class="content">投资总额（USDT）</span>
								<span class="number">{{investment}}</span>
							</view>
							<view class="pledge">
								<span class="content">我的收益（USTD）</span>
								<span class="number">{{interest}}</span>
							</view>
						</view>
						<view class="selected">
							<span>订单筛选</span>
							<view class="right-item" style="height:48upx;">
								<picker @change="pickerChange" :value="currClass" :range="classLib" mode="selector">
									<view style="padding:0upx 20upx;font-size:24upx;height:100%;background: #2D1F25;line-height: 48upx;color:#fff;display: flex;justify-content: center;align-items: center;">
										<text style="color:#999;">{{classLib[currClass]}}</text>
										<image :src="imageLib.sanjiao" style="width:20upx;height:14upx;"></image>
									</view>
								</picker>
							</view>
							</picker>
						</view>
						<view style="padding:40upx;padding-bottom:0px;">
							<block v-for="(item,index) in borrowList" :key="index">
								<view class="debitbox">
									<view class="horizon-list-item">
										<text style="font-size: 28upx;color:#fff;">{{item.status}}</text>
										<text style="color:#DA53A2;">距离还款日还有10天</text>
									</view>
									<view class="order-info">
										<span>{{item.created_on}}</span>
										<span>订单号：
											<span>{{item.id}}</span>
										</span>
									</view>
									<view class="debit-info">
										<view class="borrow">
											<span class="content">投资金额（USDT）</span>
											<span class="number">{{item.total}}</span>
										</view>
										<view class="pledge">
											<span class="content">到期收益（USDT）</span>
											<span class="number">{{item.interest}}</span>
										</view>
									</view>
									<view class="debit-btn">
										<view>
											<span class="content">综合利率</span>
											<span class="number">{{item.rate}}</span>
										</view>
										<view>
											<span class="content">周期</span>
											<span class="number">{{item.month}}</span>
										</view>
										<view>
											<span class="content">投资结束日</span>
											<span class="number">{{item.expired_on}}</span>
										</view>
									</view>
								</view>
							</block>
						</view>
					</scroll-view>
				</swiper-item>
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
				activeTab:0,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},		
				},
				imageLib:{
					sanjiao:'../../static/icons/sanjiao.png',
					add:'../../static/icons/icon_add.png',
				},
				borrowList:[{}],
				debit:0,
				mortgage:0,
				investment:0,
				interest:0,
				currClass:0,
				classLib:[
					'全部','进行中','仲裁中','已结束'
				],
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
			this.$http({
				url:'/v1/main/debit/debit-order-list',
				data:{
					type:1,
					satus:0,
					page:1
				},
				success:res=>{
					console.log(res);
					if(res.code == 200){
						this.borrowList = this.res.data.item;
						this.mortgage = this.res.data.mortgage;
						this.debit = this.res.data.debit;
						this.investment = this.res.data.investment;
						this.interest = this.res.data.interest;
					}
				}
				
			})
		},
		methods: {
			tabChange(value){
				this.activeTab = value.detail.current;
			},
			toggleTab(index){
				this.activeTab = index;
			},
			publish(){
				uni.navigateTo({
					url:'../publishborrow/publishborrow'
				})
			},
			pickerChange(e){
				this.currClass = e.target.value;
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
