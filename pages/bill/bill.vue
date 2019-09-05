<template>
	<view>
		<uni-background />
		<uni-nav-bar 
			title="我的账单" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<!-- 收益 -->
		<view class="earnbox">
			<view class="earning">
				<view class="earn-text">
					<view class="earn-img" style="width:36upx;height:36upx;margin-right: 20upx;">
						<image src="../../static/bg/dig.png" style="width:36upx;height:36upx"></image>
					</view>
					<view class="earn-pro">
						<span style="color:#fff;font-size: 28upx;font-family: Noto Sans S Chinese;">挖矿收益</span>
						<span style="color:#fff;opacity: 0.5; font-size: 22upx;font-family: Montserrat-Bold">
							<span style="margin-right: 6upx;">2019/01/24</span>
							<span>01:22</span>
						</span>
					</view>
				</view>
				<view class="earn-price" >
					<span style="color:#DA53A2;font-size: 32upx;font-weight: 600;font-family:Montserrat-Bold;margin-right:12upx;"> + 8.88</span>
					<image src="../../static/bg/to.png" style="width:24upx;height:44upx;"></image>
				</view>
			</view>
			<view class="earning">
				<view class="earn-text">
					<view class="earn-img" style="width:36upx;height:36upx;margin-right: 20upx;">
						<image src="../../static/bg/wallet.png" style="width:36upx;height:36upx"></image>
					</view>
					<view class="earn-pro">
						<span style="color:#fff;font-size: 28upx;font-family: Noto Sans S Chinese;">推广收益</span>
						<span style="color:#fff;opacity: 0.5; font-size: 22upx;font-family: Montserrat-Bold">
							<span style="margin-right: 6upx;">2019/01/24</span>
							<span>01:22</span>
						</span>
					</view>
				</view>
				<view class="earn-price" >
					<span style="color:#DA53A2;font-size: 32upx;font-weight: 600;font-family:Montserrat-Bold;margin-right:12upx;"> + 8.88</span>
					<image src="../../static/bg/to.png" style="width:24upx;height:44upx;"></image>
				</view>
			</view>
			<view class="earning">
				<view class="earn-text">
					<view class="earn-img" style="width:36upx;height:36upx;margin-right: 20upx;">
						<image src="../../static/bg/buy.png" style="width:36upx;height:36upx"></image>
					</view>
					<view class="earn-pro">
						<span style="color:#fff;font-size: 28upx;font-family: Noto Sans S Chinese;">购买矿机</span>
						<span style="color:#fff;opacity: 0.5; font-size: 22upx;font-family: Montserrat-Bold">
							<span style="margin-right: 6upx;">2019/01/24</span>
							<span>01:22</span>
						</span>
					</view>
				</view>
				<view class="earn-price" >
					<span style="color:#DA53A2;font-size: 32upx;font-weight: 600;font-family:Montserrat-Bold;margin-right:12upx;"> + 8.88</span>
					<image src="../../static/bg/to.png" style="width:24upx;height:44upx;"></image>
				</view>
			</view>
			<view class="earning">
				<view class="earn-text">
					<view class="earn-img" style="width:36upx;height:36upx;margin-right: 20upx;">
						<image src="../../static/bg/exchange.png" style="width:36upx;height:36upx"></image>
					</view>
					<view class="earn-pro">
						<span style="color:#fff;font-size: 28upx;font-family: Noto Sans S Chinese;">兑换资格</span>
						<span style="color:#fff;opacity: 0.5; font-size: 22upx;font-family: Montserrat-Bold">
							<span style="margin-right: 6upx;">2019/01/24</span>
							<span>01:22</span>
						</span>
					</view>
				</view>
				<view class="earn-price" >
					<span style="color:#DA53A2;font-size: 32upx;font-weight: 600;font-family:Montserrat-Bold;margin-right:12upx;"> + 8.88</span>
					<image src="../../static/bg/to.png" style="width:24upx;height:44upx;"></image>
				</view>
			</view>
			<view class="earning">
				<view class="earn-text">
					<view class="earn-img" style="width:36upx;height:36upx;margin-right: 20upx;">
						<image src="../../static/bg/wallet.png" style="width:36upx;height:36upx"></image>
					</view>
					<view class="earn-pro">
						<span style="color:#fff;font-size: 28upx;font-family: Noto Sans S Chinese;">转入</span>
						<span style="color:#fff;opacity: 0.5; font-size: 22upx;font-family: Montserrat-Bold">
							<span style="margin-right: 6upx;">2019/01/24</span>
							<span>01:22</span>
						</span>
					</view>
				</view>
				<view class="earn-price" >
					<span style="color:#DA53A2;font-size: 32upx;font-weight: 600;font-family:Montserrat-Bold;margin-right:12upx;"> + 8.88</span>
					<image src="../../static/bg/to.png" style="width:24upx;height:44upx;"></image>
				</view>
			</view>
			<view class="earning">
				<view class="earn-text">
					<view class="earn-img" style="width:36upx;height:36upx;margin-right: 20upx;">
						<image src="../../static/bg/change.png" style="width:36upx;height:36upx"></image>
					</view>
					<view class="earn-pro">
						<span style="color:#fff;font-size: 28upx;font-family: Noto Sans S Chinese;">转出</span>
						<span style="color:#fff;opacity: 0.5; font-size: 22upx;font-family: Montserrat-Bold">
							<span style="margin-right: 6upx;">2019/01/24</span>
							<span>01:22</span>
						</span>
					</view>
				</view>
				<view class="earn-price" >
					<span style="color:#DA53A2;font-size: 32upx;font-weight: 600;font-family:Montserrat-Bold;margin-right:12upx;"> + 8.88</span>
					<image src="../../static/bg/to.png" style="width:24upx;height:44upx;"></image>
				</view>
			</view>
			<view class="earning">
				<view class="earn-text">
					<view class="earn-img" style="width:36upx;height:36upx;margin-right: 20upx;">
						<image src="../../static/bg/wallet.png" style="width:36upx;height:36upx"></image>
					</view>
					<view class="earn-pro">
						<span style="color:#fff;font-size: 28upx;font-family: Noto Sans S Chinese;">挖矿收益</span>
						<span style="color:#fff;opacity: 0.5; font-size: 22upx;font-family: Montserrat-Bold">
							<span style="margin-right: 6upx;">2019/01/24</span>
							<span>01:22</span>
						</span>
					</view>
				</view>
				<view class="earn-price" >
					<span style="color:#DA53A2;font-size: 32upx;font-weight: 600;font-family:Montserrat-Bold;margin-right:12upx;"> + 8.88</span>
					<image src="../../static/bg/to.png" style="width:24upx;height:44upx;"></image>
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
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},		
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
	.earnbox{
		width:100%;
		padding:0 30upx;
		margin-top: 280upx;
		.earning{
			margin-top:78upx;
			display: flex;
			justify-content: space-between;
			align-items: center;
			.earn-text{
				display: flex;
				justify-content: space-between;
				.earn-pro{
					display: flex;
					flex-direction: column;
				}
			}
			.earn-price{
				display: flex;
				align-items: center;
			}
		}
	}
</style>
