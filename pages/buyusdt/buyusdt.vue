<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="买USDT" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="modal-box" v-if="showModal">
				<view class="modal">
					<view class="modal-top-item">
						<view class="modal-title">请输入您的支付密码</view>
						<view class="modal-content">
							<view class="input-box">
								<input maxlength='6' type="password">
							</view>
							<view style="font-size: 24upx;padding-top:20upx;text-align: center;">确定抵押后，您抵押的 Forest 将自动冻结</view>
						</view>
					</view>
					<view class="modal-btns">
						<view @click="showModal = false">取消</view>
						<view style="border-left:1px solid #eee;color:#0A61C9;" @click="confirmLetGo">确定</view>
					</view>
				</view>
			</view>
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button value="购买" width="670upx" large @handle="letgo()" icon="/static/icons/icon_buy_light.png"></fun-button>
				</view>
			</view>
			<view style="padding:0upx 40upx">
				<view class="horizon-list-item">
					<view class="left-item">
						<image class="left-item-avatar" :src="imageLib.union"></image>
						<text class="left-item-name">美好即将发生</text>
					</view>
					<view class="right-item">
						<text class="left-item-label">11单 · 61.11% 完成率</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">价格</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">6.6868</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">限量</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">100 - 1000</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">总金额</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">668.68 - 66868</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<image style="width:24upx;height:24upx;" class="left-item-avatar" :src="imageLib.alipay"></image>
						<image style="width:24upx;height:24upx;" class="left-item-avatar" :src="imageLib.wechatpay"></image>
						<image style="width:40upx;height:24upx;" class="left-item-avatar" :src="imageLib.unionpay"></image>
					</view>
					<view class="right-item">
						<text style="font-size: 28upx;color:#fff;">浮动价</text>
					</view>
				</view>
				<view class="fun-card" style="margin-top: 30upx;margin-bottom: 40upx;">
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item" style="width:500upx;">
								<text class="left-item-name">您想要购买多少？</text>
							</view>
						</view>
					</view>
					<view class="fun-horizen"></view>
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">USDT</text>
							</view>
							<view class="right-item">
								<input type="text" class="input-field" placeholder="输入购买数量" />
							</view>
						</view>
						<view class="horizon-list-item" style="justify-content: flex-end;">
							<view class="right-item">
								<image class="left-item-avatar" :src="imageLib.equal"></image>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">收款码</text>
							</view>
							<view class="right-item">
								<text class="left-item-name" 
								style="color:#fff;font-family:'Montserrat-Light';font-size:32upx;">39457.987</text>
							</view>
						</view>
					</view>
				</view>
				<view class="section-content" style="padding:10upx 0upx;">
					<view class="section-subtitle">留言</view>
					<view class="section-part">
						<span class="list-num">1.</span>
						请您及时付款并点击【已支付】按钮，我确认收到打款后才可以释放数字货币给您；
					</view>
					<view class="section-part">
						<span class="list-num">2.</span>
						开始交易后数字货币将有系统托管，请您安心下单；
					</view>
					<view class="section-part">
						<span class="list-num">3.</span>
						转账时请不要备注，谢谢。
					</view>
				</view>
				<view class="section-content" style="padding:10upx 0upx;">
					<view class="section-subtitle">交易提醒</view>
					<view class="section-part">
						<span class="list-num">1.</span>
						交易前请详细了解买家的交易信息；
					</view>
					<view class="section-part">
						<span class="list-num">2.</span>
						请通过平台进行沟通约定，并保存好相关聊天记录；
					</view>
					<view class="section-part">
						<span class="list-num">3.</span>
						如遇到问题，请通过“帮助”或联系客服来解决问题；
					</view>
					<view class="section-part">
						<span class="list-num">4.</span>
						您不需要支付任何手续费，交易手续费将由广告发布者承担，请安心交易；
					</view>
				</view>
			</view>
		</view>
		<view class="section-content" style="padding:10upx 0upx;background:#2D1F25;padding:20upx 40upx 150upx;margin-top:20upx;">
			<view class="section-part">
				<span class="list-num">1.</span>
				交易发起前，请您确认已阅读并同意卖家提出的条款，并再次确认交易内容无误后，再点击购买按钮；
			</view>
			<view class="section-part">
				<span class="list-num">2.</span>
				交易发起后，请您于付款期限截止前转帐至指定账户，并标记已支付，逾期系统将自动取消交易；
			</view>
			<view class="section-part">
				<span class="list-num">3.</span>
				交易发起后，系统会自动将卖家的数字货币锁定，待卖家确认收到您的转帐后，将会释放数字货币至您的账户中；
			</view>
			<view class="section-part">
				<span class="list-num">4.</span>
				交易过程请使用平台的聊天系统进行沟通，平台外的对话记录将无法作为交易纠纷的依据；
			</view>
			<view class="section-part">
				<span class="list-num">5.</span>
				温馨提示:24小时内，5分钟内无责取消机会有3次，无责取消次数用完或者订单创建超过5分钟后取消，则会被冻结5天。
			</view>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import FunButton from '@/components/fun-button.vue';
	export default{
		components:{
			UniNavBar,
			UniBackground,
			FunButton
		},
		data(){
			return {
				scroll:0,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					}
				},
				imageLib:{
					union:'../../static/avatar/fortoken.png',
					call:'../../static/icons/icon_call.png',
					alipay:'../../static/icons/icon_alipay.png',
					wechatpay:'../../static/icons/icon_wechatpay.png',
					unionpay:'../../static/icons/icon_unionpay.png',
					contact:'../../static/icons/icon_contact.png',
					equal:'../../static/icons/icon_equal.png'
				},
				showModal:false
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			letgo(){
				this.showModal = true;
			},
			confirmLetGo(){
				this.showModal = false;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.section-part{
		position: relative;
		padding-left:30upx;
		.list-num{
			position: absolute;
			line-height: 30upx;
			top:12upx;
			left:0upx;
		}
	}
	.modal-box{
		position: fixed;
		top:0px;
		left:0px;
		width:750upx;
		height:100vh;
		background: rgba(0,0,0,.5);
		z-index:1000;
		display:flex;
		justify-content:center;
		align-items:center;
		.modal{
			width:560upx;
			border-radius: 12upx;
			background: #fff;
			overflow: hidden;
			.modal-top-item{
				width:100%;
				padding:20upx 40upx;
				.modal-title{
					width:100%;
					line-height: 64upx;
					font-size: 30upx;
					color:#000;
					padding-bottom:20upx;
					text-align: center;;
				}
				.modal-content{
					width:100%;
					line-height: 48upx;
					font-size: 26upx;
					color:#000;
					.input-box{
						width:100%;
						display:flex;
						justify-content:center;
						align-items:center;
						
						input{
							display: block;
							width:300upx;
							height:64upx;
							line-height: 64upx;
							color:#DA53A2;
							background: #F2F8FF;
							text-align: center;
							font-weight: bold;
							font-size: 36upx;
							font-family:'Montserrat-Bold';
						}
					}
				}
			}
			.modal-btns{
				border-top:1px solid #eee;
				width:100%;
				display: flex;
				justify-content: space-between;
				view{
					width:50%;
					line-height: 100upx;
					height:100upx;
					color:#000;
					text-align: center;
					font-size: 32upx;
					&:active{
						background: #eee;
					}
				}
			}
		}
	}
	.fun-card-item{
		padding:20upx 30upx;
	}
	.order-btn{
		width:132upx;
		height:64upx;
		background: #DA53A2;
		border-radius: 32upx;
		display: flex;
		justify-content: center;
		align-items: center;
		image{
			width:32upx !important;
			height:32upx !important;
			margin:0px !important;
		}
	}
	.horizon-list-item{
		padding:10upx 0upx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		.left-item{
			display:flex;
			justify-content:flex-start;
			align-items:center;
			.left-item-avatar{
				width:40upx;
				height:40upx;
				margin-right:20upx;
			}
			.left-item-name{
				color:#fff;
				font-size: 26upx;
				padding-right:15upx;
			}
			.left-item-label{
				color:#999;
				font-size: 24upx;
				margin-right: 18upx;
			}
			.left-item-title{
				display: block;
				color:#fff;
				font-size: 32upx;
				line-height: 52upx;
				font-family:'Montserrat-Bold';
				span{
					font-family:'Montserrat-Bold';
				}
			}
			.left-item-date{
				display: block;
				color:#999;
				font-size: 26upx;
				line-height: 52upx;
				font-family:'Montserrat-Light';
			}
		}
		.right-item{
			display:flex;
			justify-content:flex-end;
			align-items:center;
			color:#999;
			font-size: 24upx;
			.input-field{
				width:220upx;
				text-align: right;
				color:#DA53A2;
				font-size: 28upx;
				font-weight:bold;
			}
			.left-item-name{
				color:#fff;
				font-size: 26upx;
			}
			.right-item-text{
				font-size: 38upx;
				color:#56CCF2;
				font-family:'Montserrat-Bold';
				span{
					font-family:'Montserrat-Bold';
				}
			}
			image{
				width:42upx;
				height:42upx;
				margin-left:10upx;
			}
		}
	}
</style>