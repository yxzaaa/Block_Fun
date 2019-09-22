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
					<text :class="{active:activeTab == 0}" @click="toggleTab(0)">借款挂单</text>
				</view>
				<view class="fix-tabs-item">
					<text :class="{active:activeTab == 1}" @click="toggleTab(1)">投资挂单</text>
				</view>
			</view>
			<swiper class="swiper-box" :current="activeTab" @change="tabChange">
				<swiper-item>
					<scroll-view scroll-y='true' style="width:100%;height:100%;">
						<view style="padding:40upx;padding-bottom:0px;">
							<block v-for="(item,index) in borrowList" :key="index">
								<view class="debitbox">
									<view class="horizon-list-item">
										<text>2019/03/15 19:00</text>
										<text style="color:#DA53A2;">已发布</text>
									</view>
									<view class="debit-info">
										<view class="debit">
											<span class="text">USDT价格</span>
											<span class="number">0.168</span>
										</view>
										<view class="debit">
											<span class="text">投资总量</span>
											<span class="number">800</span>
										</view>
										<view class="debit">
											<span class="text">月利率</span>
											<span class="number">0.1
												<span>%</span>
											</span>
										</view>
										<view class="debit">
											<span class="text">月</span>
											<span class="number">
												30 <span>天</span>
											</span>
										</view>
									</view>
									<view class="debit-btn">
										<text>七天后过期</text>
										<navigator :url="'../borrowpage/borrowpage?id='+index">
											<view>下架</view>
										</navigator>
									</view>
								</view>
							</block>
						</view>
					</scroll-view>
				</swiper-item>
				<swiper-item>
					<scroll-view scroll-y='true' style="width:100%;height:100%;">
						<view style="padding:40upx;padding-bottom:0px;">
							<block v-for="(item,index) in investList" :key="index">
								<view class="debitbox">
									<view class="horizon-list-item">
										<text>2019/03/15 19:00</text>
										<text style="color:#DA53A2;">已发布</text>
									</view>
									<view class="debit-info">
										<view class="debit">
											<span class="text">USDT价格</span>
											<span class="number">0.168</span>
										</view>
										<view class="debit">
											<span class="text">投资总量</span>
											<span class="number">800</span>
										</view>
										<view class="debit">
											<span class="text">月利率</span>
											<span class="number">0.1
												<span>%</span>
											</span>
										</view>
										<view class="debit">
											<span class="text">月</span>
											<span class="number">
												30 <span>天</span>
											</span>
										</view>
									</view>
									<view class="debit-btn">
										<text>七天后过期</text>
										<navigator :url="'../investpage/investpage?id='+index">
											<view>下架</view>
										</navigator>
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
					add:'../../static/icons/icon_add.png',
				},
				borrowList:[
					{},{},{},{}
				],
				investList:[
					{},{},{}
				]
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
			width:100%;
			padding:40upx;
			display: flex;
			justify-content: space-between;
			border-bottom:1px solid rgba(255,255,255,0.1);
			.debit{
				display: flex;
				flex-direction: column;
				justify-content: space-between;
				text-align:center;
				.text{
					font-size: 24upx;				
					color: #FFFFFF;					
					opacity: 0.5;
					span{
						font-size: 24upx;					
						color: #FFFFFF;
						margin-left:12upx;
					}
				}
				.number{
					margin-top:14upx;
					font-family: 'Montserrat-Bold';
					font-style: normal;
					font-weight: 600;
					font-size: 40upx;
					color: #FFFFFF;
					span{
						font-size: 22upx;					
						color: #FFFFFF;
						margin-left:8upx;
					}
				}
			}
		}
		.debit-btn{
			width:670upx;
			padding:30upx 40upx;
			display:flex;
			justify-content:space-between;
			align-items:center;
			text{
				color:#DA53A2;
				font-size: 24upx;
			}
			view{
				width:192upx;
				background: #DA53A2;
				border-radius: 200upx;
				text-align: center;
				line-height: 64upx;
				color: #FEFEFE;
				font-size: 28upx;
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
</style>
