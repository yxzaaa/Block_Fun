<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			title="抵押借贷" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full">
			<view class="fiexd-btn" @click="publish()">
				<image :src="imageLib.add"></image>
			</view>
			<view class="fixed-drop-btn">
				<image class="btn" src="../../static/icons/icon_drop.png" @click="toggleDropDown"></image>
				<view class="dropdown" v-if="dropShow">
					<navigator url="../billorders/billorders" style="width:100%;padding:24upx 0;display: flex;align-items: center;">
						<image src="/static/icons/icon_dingdan.png" style="width:40upx;height:40upx;margin-right:20upx;"></image>
						<text style="font-size: 28upx;color:#DA53A2">我的订单</text>
					</navigator>
					<view style="width:100%;height:2upx;background: #E2E2E2;"></view>
					<navigator url="../mytransbill/mytransbill" style="width:100%;padding:24upx 0;display: flex;align-items: center;">
						<image src="/static/icons/icon_guadan.png" style="width:40upx;height:40upx;margin-right:20upx;"></image>
						<text style="font-size: 28upx;color:#DA53A2">我的挂单</text>
					</navigator>
				</view>
			</view>
			<view class="fix-tabs-box">
				<view class="fix-tabs-item">
					<text :class="{active:activeTab == 1}" @click="toggleTab(1)">我要借款</text>
				</view>
				<view class="fix-tabs-item">
					<text :class="{active:activeTab == 2}" @click="toggleTab(2)">我要投资</text>
				</view>
			</view>
			<scroll-view scroll-y='true' style="width:100%;height:calc(100vh - 274upx);">
				<view style="padding:40upx;padding-bottom:0px;">
					<block v-for="(item,index) in borrowList" :key="index">
						<view class="debitbox">
							<view class="debit-info">
								<view class="debit">
									<span class="text">USDT价格</span>
									<span class="number">{{getNum(item.price)}}</span>
								</view>
								<view class="debit">
									<span class="text">投资总量</span>
									<span class="number">{{getNum(item.total)}}</span>
								</view>
								<view class="debit">
									<span class="text">月利率</span>
									<span class="number">{{item.rate*100}}
										<span>%</span>
									</span>
								</view>
								<view class="debit">
									<span class="text">月</span>
									<span class="number">
										{{item.month}}<span>月</span>
									</span>
								</view>
							</view>
							<view class="debit-btn">
								<view @click="acceptBill(item)">{{item.type == 1?'借款':'投资'}}</view>
							</view>
						</view>
					</block>
				</view>
			</scroll-view>
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
				activeTab:1,
				currPage:1,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},		
				},
				imageLib:{
					add:'../../static/icons/icon_add.png',
				},
				borrowList:[],
				dropShow:false
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
			this.updateList();
		},
		methods: {
			//请求挂单列表
			updateList(){
				uni.showLoading({
					title:"挂单加载中..."
				})
				this.$http({
					url:'/v1/main/debit/debit-list',
					data:{
						type:this.activeTab,
						page:this.currPage
					},
					success:res=>{
						console.log(res);
						if(res.code == 200){
							uni.hideLoading();
							this.borrowList = res.data.item;
						}
					}
				})
			},
			//接受挂单
			acceptBill(item){
				uni.setStorage({
					key:'accept_bill_info',
					data:item,
					success:res=>{
						uni.navigateTo({
							url:'../borrowpage/borrowpage'
						})
					}
				})
			},
			getNum(num){
				return (parseFloat(num)).toFixed(2);
			},
			toggleDropDown(){
				this.dropShow = this.dropShow?false:true;
			},
			toggleTab(index){
				this.activeTab = index;
				this.updateList();
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
	.fixed-drop-btn{
		position: fixed;
		top:210upx;
		right:40upx;
		z-index:90;
		&:focus{
			outline:none;
			.dropdown{
				display: block;
			}
		}
		.btn{
			position: absolute;
			top:0px;
			right:0px;
			width:40upx;
			height:40upx;
		}
		.dropdown{
			position:absolute;
			top:50upx;
			right:-18upx;
			width:260upx;
			height:250upx;
			padding:40upx;
			z-index:99;
			background: url('../../static/icons/drop_bg.png') 100% 100%;
			background-size:100% 100%;
		}
	}
	.debitbox{
		width:670upx;
		background: rgba(45, 31, 37,0.8);
		border-radius: 10px;
		margin-bottom:30upx;
		.debit-info{
			width:100%;
			padding:40upx;
			display: flex;
			justify-content: space-between;
			border-bottom:1px solid rgba(255,255,255,0.2);
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
			padding:29upx 40upx 30upx 438upx;
			display:flex;
			justify-content:flex-end;
			
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
