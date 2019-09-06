<template>
	<view>
		<uni-background />
		<uni-nav-bar 
			title="抵押借贷" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="debitbox" style="margin-top:280upx;">
			<view class="debit-info">
				<view class="debit">
					<span class="text">单价USDT</span>
					<span class="number">0.168</span>
				</view>
				<view class="debit">
					<span class="text">投资USDT</span>
					<span class="number">800</span>
				</view>
				<view class="debit">
					<span class="text">日利率</span>
					<span class="number">0.1
						<span>%</span>
					</span>
				</view>
				<view class="debit">
					<span class="text">周期</span>
					<span class="number">
						30 <span>天</span>
					</span>
				</view>
			</view>
			<view class="debit-btn">
				<button>借款</button>
			</view>
		</view>
		<view class="debitbox">
			<view class="debit-info">
				<view class="debit">
					<span class="text">单价USDT</span>
					<span class="number">0.168</span>
				</view>
				<view class="debit">
					<span class="text">投资USDT</span>
					<span class="number">800</span>
				</view>
				<view class="debit">
					<span class="text">日利率</span>
					<span class="number">0.1
						<span>%</span>
					</span>
				</view>
				<view class="debit">
					<span class="text">周期</span>
					<span class="number">
						30 <span>天</span>
					</span>
				</view>
			</view>
			<view class="debit-btn">
				<button>借款</button>
			</view>
		</view>
		<view class="debitbox">
			<view class="debit-info">
				<view class="debit">
					<span class="text">单价USDT</span>
					<span class="number">0.168</span>
				</view>
				<view class="debit">
					<span class="text">投资USDT</span>
					<span class="number">800</span>
				</view>
				<view class="debit">
					<span class="text">日利率</span>
					<span class="number">0.1
						<span>%</span>
					</span>
				</view>
				<view class="debit">
					<span class="text">周期</span>
					<span class="number">
						30 <span>天</span>
					</span>
				</view>
			</view>
			<view class="debit-btn">
				<button>借款</button>
			</view>
		</view>
		<view class="debitbox">
			<view class="debit-info">
				<view class="debit">
					<span class="text">单价USDT</span>
					<span class="number">0.168</span>
				</view>
				<view class="debit">
					<span class="text">投资USDT</span>
					<span class="number">800</span>
				</view>
				<view class="debit">
					<span class="text">日利率</span>
					<span class="number">0.1
						<span>%</span>
					</span>
				</view>
				<view class="debit">
					<span class="text">周期</span>
					<span class="number">
						30 <span>天</span>
					</span>
				</view>
			</view>
			<view class="debit-btn">
				<button>借款</button>
			</view>
		</view>
		<view class="debitbox">
			<view class="debit-info">
				<view class="debit">
					<span class="text">单价USDT</span>
					<span class="number">0.168</span>
				</view>
				<view class="debit">
					<span class="text">投资USDT</span>
					<span class="number">800</span>
				</view>
				<view class="debit">
					<span class="text">日利率</span>
					<span class="number">0.1
						<span>%</span>
					</span>
				</view>
				<view class="debit">
					<span class="text">周期</span>
					<span class="number">
						30 <span>天</span>
					</span>
				</view>
			</view>
			<view class="debit-btn">
				<button>借款</button>
			</view>
		</view>
		<view class="addbtn" style="width:96upx;height:96upx;">
			<image src="../../static/bg/addbtn.png" style="width:96upx;height:96upx;"></image>
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
	.debitbox{
		width:670upx;
		height:310upx;
		background: rgba(45, 31, 37,0.8);
		border-radius: 10px;
		margin:40upx 40upx 0;
		.debit-info{
			width:100%;
			height:186upx;
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
					font-family: PingFang SC;
					font-size: 22upx;				
					color: #FFFFFF;					
					opacity: 0.5;
					span{
						font-family: PingFang SC;
						font-size: 22upx;					
						color: #FFFFFF;
						margin-left:12upx;
					}
				}
				.number{
					margin-top:14upx;
					font-family: Montserrat;
					font-style: normal;
					font-weight: 600;
					font-size: 40upx;
					color: #FFFFFF;
					span{
						font-family: PingFang SC;
						font-size: 22upx;					
						color: #FFFFFF;
						margin-left:12upx;
					}
				}
			}
		}
		.debit-btn{
			width:670upx;
			height:123upx;
			padding:29upx 40upx 30upx 438upx;
			display:flex;
			justify-content:flex-end;
			
			button{
				width:192upx;
				height:64upx;
				background: #DA53A2;
				border-radius: 200upx;
				text-align: center;
				line-height: 64upx;
				color: #FEFEFE;
				font-size: 28upx;
				font-family: Noto Sans S Chinese;
			}
			
		}
	}
	.addbtn{
		position: fixed;
		bottom:136upx;
		right:70upx;
	}
</style>
