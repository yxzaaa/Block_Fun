<template>
	<view>
		<uni-background :src="imageLib.bg"/>
		<uni-nav-bar 
			title="我的财务" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view style="margin:220upx 30upx 0;font-size:24upx;font-family: Noto Sans S Chinese;color:#fff;opacity: 0.5;">
			总资产
		</view>
		<view class="fortune" style="display: flex;justify-content: space-between;width:750upx;padding:0 30upx;margin-top: 16upx;align-items: flex-end;">
			<span>
				<span style="font-size: 36upx;color:#fff;font-family: Montserrat-Bold;margin-right:10upx;">$</span>
				<span style="font-size: 60upx;color:#fff;font-family: Montserrat-Bold">6888.68</span>
			</span>
			<span style="font-size:24upx;font-family: Noto Sans S Chinese;color:#fff;opacity: 0.5;">资产类型3种</span>
		</view>
		<view class="fortunetype">
			<view style="font-size:32upx;font-family: PingFang SC;color:#fff;margin:116upx 30upx 0;">
				资产类型：<span>矿机</span>
			</view>
			<view class="typeinfo">
				<view>
					<span class="type">矿机型号</span>
					<span class="numb">Forest</span>
				</view>
				<view>
					<span class="type">矿机数量</span>
					<span class="numb">10</span>
				</view>
				<view>
					<span class="type">矿机总价值<span style="font-size: 20upx;margin-left:10upx;">($)</span>
					</span>
					<span class="numb">16000</span>
				</view>
			</view>
		</view>
		<view class="fortunetype">
			<view style="font-size:32upx;font-family: PingFang SC;color:#fff;margin:0 30upx 0;">
				资产类型：<span>USDT</span>
			</view>
			<view class="typeinfo">
				<view>
					<span class="type">币种</span>
					<span class="numb">USDT</span>
				</view>
				<view>
					<span class="type">矿机数量</span>
					<span class="numb">10</span>
				</view>
				<view>
					<span class="type">币种总价值<span style="font-size: 20upx;margin-left:10upx;">($)</span>
					</span>
					<span class="numb">16000</span>
				</view>
			</view>
		</view>
		<view class="fortunetype">
			<view style="font-size:32upx;font-family: PingFang SC;color:#fff;margin:0 30upx 0;">
				资产类型：<span>运算力</span>
			</view>
			<view class="typeinfo">
				<view>
					<span class="type">运算力</span>
					<span class="numb">xxx</span>
				</view>
				<view>
					<span class="type">矿机数量</span>
					<span class="numb">10</span>
				</view>
				<view>
					<span class="type">资产总价值<span style="font-size: 20upx;margin-left:10upx;">($)</span>
					</span>
					<span class="numb">16000</span>
				</view>
			</view>
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
				imageLib:{
					bg:'../../static/bg2.jpg'
				},
				navButtons:{
					back:{
						type:'normal'
					},
					textbtn:{
						text:'账单',
						url:'../bill/bill'
					}
				}
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods: {
			
		}
	}
</script>

<style lang="scss" scoped>
	.typeinfo{
		width:690upx;
		height:212upx;
		margin:24upx 30upx 54upx;
		padding:34upx 36upx 42upx 38upx;
		background: #2D1F25;
		display: flex;
		justify-content: space-between;
		view{
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: space-between;
			.type{
				font-family: PingFang SC;
				font-size: 28upx;
				color: #FFFFFF;			
				opacity: 0.5;
			}
			.numb{
				font-family: Montserrat;
				font-style: normal;
				font-weight: 600;
				font-size: 28upx;
				color: #FFFFFF;
			}
		}
	}
</style>
