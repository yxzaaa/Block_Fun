<template>
	<view>
		<uni-background />
		<uni-nav-bar 
			title="信任转让" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="currency-box">
			<span style="color:#fff;opacity: 0.5;font-size: 24upx;">币种</span>
			<view class="text">
				<image src="../../static/bg/tree.png"></image>
				<span style="color:#fff;font-size: 26upx;margin-left:20upx;">Forbidden Forest Coin</span>
				<span style="color:#fff;font-size: 26upx;padding-left:10upx;border-left:1px solid rgba(255,255,255,0.5);margin-left:16upx;">Forest</span>
			</view>
		</view>
		<view class="assignment-box">
			<view class="Uid">
				<span>UID</span>
				<input type="text" value="请输入对方UID">
			</view>
			<view class="assignment-number">
				<span class="number">转让数量</span>
				<view>
					<input type="text" value="可用余额 100 Xday">
					<span class="button">全部转出</span>
				</view>
				<span class="upper-limit">每次转出上限100</span>
			</view>
			<view class="add-remark">
				<span>添加备注</span>
				<input type="text" value="点击添加">
			</view>
		</view>
		<view class="confirm-btn">
			确认转让
		</view>
		<view class="invite">
			<image src="../../static/bg/add.png"></image>
			<span>先去邀请好友</span>
		</view>
		<view class="flow-box">
			<span>操作流程</span>
			<view class="flow">
				<span>1</span>
				<image src="../../static/bg/line.png"></image>
				<span>2</span>
				<image src="../../static/bg/line.png"></image>
				<span>3</span>
			</view>
			<view class="text">
				<span>邀请好友注册</span>
				<span>转让给好友 N 枚 Xdag</span>
				<span>自己获得 N 枚 Xdag</span>
			</view>
		</view>
		<view class="active-info">
			<view class="info">活动细则</view>
			<view class="content">
				<span>
					<span class="number" style="line-height: 44upx;">1.</span>
					<span class="text" style="line-height: 44upx;">每邀请1位新用户注册成功，并且转给你邀请的用户N枚Xdag，你将获得N枚Xdag</span>
				</span>
				<span>
					<span class="number">2.</span>
					<span class="text">每次转出上限100枚，每个账户有10次转出名额</span>
				</span>
				<span>
					<span class="number">3.</span>
					<span class="text">转出成功后，收益立即到账</span>
				</span>
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
	.currency-box{
		width:670upx;
		height:96upx;
		margin:176upx 30upx 0;
		padding:0 44upx 0 40upx;
		display: flex;
		justify-content: space-between;
		align-items:center;
		view{
			image{
				width:32upx;
				height:32upx;
			
			}
		}
	}
	.assignment-box{
		width:670upx;
		height:692upx;
		background: rgba(45, 31, 37,0.8);
		border-radius: 10px 10upx 0 0;
		margin:0 40upx 0;
		padding:60upx 30upx 0;
		.Uid{
			width:590upx;
			height:129upx;
			border-bottom:1px solid rgba(255,255,255,0.1);
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			span{
				font-size: 28upx;
				color: #FFFFFF;
			}
			input{
				font-family: Noto Sans S Chinese;
				font-size: 24upx;
				color: #FFFFFF;			
				opacity: 0.5;
				margin-bottom:18upx;
			}
		}
		.assignment-number{
			width:590upx;
			height:176upx;
			margin-top:61upx;
			.number{
				font-size: 28upx;
				color: #FFFFFF;
			}
			view{
				margin-top:34upx;
				display:flex;
				justify-content:space-between;
				border-bottom:1px solid rgba(255,255,255,0.1);
				input{
					font-size: 24upx;
					color: #FFFFFF;			
					opacity: 0.5;
					margin-bottom:18upx;
				}
				.button{
					font-size: 26upx;
					color: #DA53A2;
				}
			}
			.upper-limit{
				font-size: 24upx;
				color: #FFFFFF;			
				opacity: 0.5;
			}
		}
		.add-remark{
			width:610upx;
			height:148upx;
			margin-top:58upx;
			span{
				font-size: 28upx;
				color: #FFFFFF;
			}
			input{
				width:610upx;
				height:88upx;
				background: #15030B;
				border-radius: 10upx;
				padding:28upx 0 24upx 30upx;
				font-size: 26upx;
				color: #FFFFFF;
				opacity: 0.5;
				margin-top:20upx;
			}
		}
	}
	.confirm-btn{
		width:670upx;
		height:100upx;
		text-align: center;
		line-height: 100upx;
		background: rgba(218, 83, 162,0.3);
		color:#DA53A2;
		font-size: 16px;
		margin:0 40upx;
		border-radius:0 0 10upx 10upx;
	}
	.invite{
		width:220upx;
		height:42upx;
		margin:44upx 276upx 58upx 254upx;
		display:flex;
		justify-content:space-between;
		align-items:center;
		image{
			width:32upx;
			height:32upx;
		}
		span{
			font-size: 28upx;
			color: #DA53A2;
		}
	}
	.flow-box{
		width:100%;
		height:202upx;
		display: flex;
		justify-content:center;
		flex-direction: column;
		margin-top:58upx;
		span{
			margin:0 auto;
			font-size: 28upx;
			color: #FFFFFF;
		}
		.flow{
			display: flex;
			margin-top:60upx;
			align-items:center;
			padding:0 104upx 0 98upx;
			image{
				width:175upx;
				height:2upx;
			}
			span{
				width:48upx;
				height:48upx;
				border:6upx solid #fff;
				border-radius: 50%;
				text-align: center;
				line-height:48upx;
			}
		}
		.text{
			padding:0 0 0 45upx;
			margin-top:30upx;
			display: flex;
			span{
				font-size: 20upx;
				text-align: center;			
				color: #FFFFFF;
				opacity: 0.5;
			}
		}
	}
	.active-info{
		width:100%;
		height:294upx;
		margin-top:58upx;
		border-top:1px solid rgba(255,255,255,0.2);
		padding:59upx 40upx 0;
		margin-bottom:122upx;
		.info{
			font-size: 26upx;	
			color: #FFFFFF;
			opacity: 0.5;
			marign-bottom:20upx;
		}
		.content{
			widht:335upx;
			display: flex;
			flex-direction: column;
			span{
				display: flex;
				span{
					font-size: 24upx;
					color:#fff;
					opacity: 0.5;
					line-height:36upx;
					margin-top:10upx;
				}
				.number{
					margin-right:10upx;
				}
			}
		}
	}
</style>
