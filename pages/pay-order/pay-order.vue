<template>
	<view class="container">	
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="支付订单"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full">
			<view class="payNumber">
				<view class="symbolNumber">
					<span class="symbol">￥</span>
					<span class="price">{{amountCount}}</span>
				</view>
			</view>
			<view class="payStyle">
				<view class="cash">
					<span class="content">
						现金支付
					</span>
					<span class="number">
						<span>
							￥{{amountCount}}
						</span>
						<image src="../../static/bg/check.png" style="width:32upx;height:32upx;margin-left:16upx;"></image>
					</span>
				</view>
				<!-- <view class="integral">
					<span class="content">
						积分支付
					</span>
					<span class="number">
						<span style="font-size:28upx;color:#C7C7C7">
							4000
						</span>
						<image src="../../static/bg/checkbox.png" style="width:32upx;height:32upx;margin-left:16upx;"></image>
					</span>
				</view> -->
			</view>
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button :value="'现金支付 ￥'+amountCount" width="670upx" large @handle="showModal = true"></fun-button>
				</view>
			</view>
			<view class="modal-box" v-if="showModal">
				<view class="modal">
					<view class="modal-top-item">
						<view class="modal-title">请输入您的支付密码</view>
						<view class="modal-content">
							<possword-inputer @input="setPassword" :value="payPassword"></possword-inputer>
						</view>
					</view>
					<view class="modal-btns">
						<view @click="showModal = false">取消</view>
						<view style="border-left:1px solid #eee;color:#0A61C9;" @click="payOrder">支付</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import FunButton from '@/components/fun-button.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import PosswordInputer from '@/components/possword-inputer.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			FunButton,
			PosswordInputer
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
				amountCount:'',
				orderId:'',
				showModal:false,
				payPassword:'',
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(option){
			this.orderId = option.id;
			this.amountCount = option.amount;
		},
		methods: {
			//设置密码
			setPassword(val){
				this.payPassword = val;
			},
			//订单支付
			payOrder(){
				console.log(this.payPassword);
				if(this.payPassword.length === 8){
					this.$http({
						url:'/order/pay',
						type:'application/x-www-form-urlencoded',
						data:{
							item:this.orderId,
							password:this.payPassword
						},
						success:res=>{
							if(res.code == 200){
								this.showModal = false;
								uni.navigateTo({
									url:'../pay-result/pay-result?id='+this.orderId
								})
							}else{
								uni.showToast({
									title:res.message,
									icon:'none'
								})
							}
						}
					})
				}else{
					uni.showToast({
						title:"请输入8位支付密码",
						icon:'none'
					})
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.payNumber{
		width:750upx;
		padding:80upx 0upx;
		padding-top:60upx;
		display:flex;
		justify-content:center;
		.symbolNumber{
			width:264upx;
		}
		.symbol{
			font-size:36upx;
			font-family:'Montserrat-Bold';
			color:#DA53A2;
			font-weight: 600;
			margin-right:10upx;
		}
		.price{
			font-size:56upx;
			font-family:'Montserrat-Bold';
			color:#DA53A2;
			font-weight: 600;
		}
	}
	.payStyle{
		width:670upx;
		background:#2D1F25;
		padding:40upx;
		border-radius: 8upx;
		margin:auto;
		display: flex;
		flex-direction: column;
		align-content:start;
		.cash{
			display: flex;
			justify-content: space-between;
			
		}
		.number{
			
			display: flex;
			align-items: center;
			span{
				font-size:28upx;
				color:#DA53A2;
				font-weight:bold;
				font-family:'Montserrat-Bold';
			}
		}
		.integral{
			display: flex;
			justify-content: space-between;
			margin-top:50upx;
		}
		.content{
			color:#fff;
			font-size: 28upx;
		}
	}
	.button-group{
		width:670upx;
	}
</style>
