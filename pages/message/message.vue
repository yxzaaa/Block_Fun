<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="提交留言" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="fun-card" style="margin:30upx 40upx;width:670upx;">
				<view class="fun-card-item">
					<textarea name="" id="" cols="30" rows="10" style="color:#fff;font-size: 32upx;" maxlength="100" @input="checkLength"></textarea>
					<view style="color:#999;text-align: right;font-size: 24upx;">{{length}} / {{max}}</view>
				</view>
				<view class="submit-btn" @click="saveMessage">
					留言
				</view>
			</view>
			<view style="padding-top:60upx;">
				<view style="font-size: 28upx;color:rgba(255,255,255,0.5);text-align: center;">留言快捷选择</view>
				<view class="quick-list">
					<view>请看到留言后，尽快支付</view>
					<view>请选择银行卡支付吧</view>
					<view>请选择支付宝支付吧</view>
					<view>我未收到打款，已申请仲裁</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import FunButton from '@/components/fun-button.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
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
				message:'',
				length:0,
				max:100
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			checkLength(e){
				this.length = e.detail.value.length;
				if(this.length<=this.max){
					this.message = e.detail.value;
				}
			},
			saveMessage(){
				uni.navigateBack({
					delta:1
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.quick-list{
		width:750upx;
		padding:40upx;
		padding-top:20upx;
		view{
			width:670upx;
			height:88upx;
			background: #2D1F25;
			border-radius: 44upx;
			color:#fff;
			font-size: 32upx;
			line-height: 88upx;
			text-align: center;
			margin:15upx 0upx;
		}
	}
	.handler-status{
		padding:30upx 0upx;
		.right-status{
			text{
				display: inline-block;
			}
		}
	}
	.user-info{
		width:750upx;
		display:flex;
		justify-content:center;
		align-items:center;
		padding:20upx 0;
		image{
			width:48upx;
			height:48upx;
			margin-right:20upx;
		}
		text{
			color:#fff;
			font-size: 32upx;
		}
	}
	.user-count{
		width:750upx;
		text-align:center;
		padding:30upx 0;
		text{
			color:#DA53A2;
			font-size: 52upx;
			font-family:'Montserrat-Bold';
		}
	}
	.erweima{
		width:200upx;
		height:200upx;
		background: #fff;
		border-radius: 12upx;
		margin:auto;
		padding:20upx;
		image{
			width:100%;
			height:100%;
		}
	}
</style>
