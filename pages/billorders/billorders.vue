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
			<scroll-view scroll-y='true' style="width:100%;height:calc(100vh - 274upx);">
				<view class="totalBox">
					<view class="borrow">
						<span class="content">投资总额（USDT）</span>
						<span class="number">5000</span>
					</view>
					<view class="pledge">
						<span class="content">我的收益（USTD）</span>
						<span class="number">100000</span>
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
								<text style="font-size: 28upx;color:#fff;">进行中</text>
								<text style="color:#DA53A2;">距离还款日还有10天</text>
							</view>
							<view class="order-info">
								<span>2019/03/15 19:00</span>
								<span>订单号：
									<span>asdasdasdasd</span>
								</span>
							</view>
							<view class="debit-info">
								<view class="borrow">
									<span class="content">投资金额（USDT）</span>
									<span class="number">5000</span>
								</view>
								<view class="pledge">
									<span class="content">到期收益（USDT）</span>
									<span class="number">100000</span>
								</view>
							</view>
							<view class="debit-btn">
								<view>
									<span class="content">综合利率</span>
									<span class="number">1.5%</span>
								</view>
								<view>
									<span class="content">周期</span>
									<span class="number">15天</span>
								</view>
								<view>
									<span class="content">投资结束日</span>
									<span class="number">2019/4/12</span>
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
				activeTab:0,
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
				borrowList:[
					{},{},{},{}
				],
				investList:[
					{},{},{}
				],
				currClass:0,
				classLib:[
					'全部','进行中','仲裁中','已结束'
				],
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
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
