<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="订单详情" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full fixbutton">
			<view class="modal-box" v-if="showModal">
				<view class="modal">
					<view class="modal-top-item">
						<view class="modal-title">请输入您的支付密码</view>
						<view class="modal-content">
							<possword-inputer></possword-inputer>
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
					<fun-button value="申请仲裁" width="320upx" type="light" large url="../autolock/autolock"></fun-button>
					<fun-button value="点击放行" width="320upx" large @handle="letgo()"></fun-button>
				</view>
			</view>
			<view style="padding:0upx 40upx">
				<view class="fun-card">
					<view class="fun-card-item" style="padding:20upx;">
						<view class="horizon-list-item" style="justify-content: center;">
							<text style="color:rgba(255,255,255,0.5);font-size:24upx;">对方将订单标记为 "已支付"，请尽快点击【放行】</text>
						</view>
					</view>
				</view>
				<view class="main-title" style="text-align: left;">进行中</view>
				<view class="fun-horizen" style="margin-bottom:20upx;"></view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">订单编号</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">2A4EF9Q3FA8WDAMW19Z668PAFR</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">创建时间</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">2019/01/28 20:35</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">价格</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">6.6868 CNY</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">限额</text>
					</view>
					<view class="right-item">
						<text class="left-item-name">100 USDT</text>
					</view>
				</view>
				<view class="horizon-list-item">
					<view class="left-item">
						<text class="left-item-label">总金额</text>
					</view>
					<view class="right-item">
						<text style="font-size: 40upx;color:#fff;font-family: 'Montserrat-Bold';">668.68 CNY</text>
					</view>
				</view>
				<view class="fun-card" style="margin-top:20upx;">
					<view class="fun-card-item" style='padding:20upx 30upx;'>
						<view class="horizon-list-item">
							<view class="left-item">
								<image class="left-item-avatar" :src="imageLib.union"></image>
								<text class="left-item-name">美好即将发生</text>
							</view>
							<view class="right-item">
								<view class="button-group" style="width:300upx;">
									<view class="order-btn">
										<image :src="imageLib.call"></image>
									</view>
									<view class="order-btn">
										<image :src="imageLib.contact"></image>
									</view>
								</view>
							</view>
						</view>
					</view>
				</view>
				<view class="fun-card" style="margin-top: 30upx;margin-bottom: 40upx;">
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item" style="width:500upx;">
								<text class="left-item-name">收款信息</text>
							</view>
							<view class="right-item">
								<text class="left-item-label">微信</text>
							</view>
						</view>
					</view>
					<view class="fun-horizen"></view>
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">账号</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">15816168188</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">姓名</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">王大锤</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">收款码</text>
							</view>
							<view class="right-item">
								<text class="left-item-name" style="color:#DA53A2">点击查看</text>
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
						请您及时在订单有效期内付款并点击【已支付】按钮，避免超时自动放单造成的财产损失；
					</view>
					<view class="section-part">
						<span class="list-num">2.</span>
						请通过平台进行沟通约定，并保存好相关聊天记录；
					</view>
					<view class="section-part">
						<span class="list-num">3.</span>
						如遇到问题，请通过“帮助”或联系客服来解决问题；
					</view>
				</view>
				<view style="width:200upx;margin:20upx auto">
					<fun-button value="联系客服" type="text" color="#DA53A2" large width="200upx" icon="../../static/icons/Shape.png"></fun-button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import FunButton from '@/components/fun-button.vue';
	import PosswordInputer from '@/components/possword-inputer.vue';
	export default{
		components:{
			UniNavBar,
			UniBackground,
			FunButton,
			PosswordInputer
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
					contact:'../../static/icons/icon_contact.png',
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
			.left-item-name{
				color:#fff;
				font-size: 26upx;
				padding-right:15upx;
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