<template>
	<view class="container">
		<uni-background src="../../static/bg1.jpg"/>
		<uni-nav-bar title="邀请好友" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button value="复制链接" width="320upx" type="light" large url="../autolock/autolock"></fun-button>
					<fun-button value="生成邀请卡" width="320upx" large url="../invitefriends/invitefriends"></fun-button>
				</view>
			</view>
			<view style="padding:0upx 40upx;padding-bottom:150upx;">
				<view class="fun-card-item">
					<view class="lock-total-box">
						<view class="lock-item-box">
							<view class="lock-item">
								<text class="text-vertical-top">我的邀请码</text>
								<text class="text-vertical-bottom">W6GRWQ</text>
							</view>
							<view class="lock-item-block">
								复制
							</view>
						</view>
						<view class="lock-item-box">
							<view class="lock-item">
								<text class="text-vertical-top">锁仓激活码</text>
								<text class="text-vertical-bottom">H6GJ9Q</text>
							</view>
							<view class="lock-item-block">
								复制
							</view>
						</view>
					</view>
					<view style="padding-top:10upx;padding-left:36upx;position: relative;">
						<image :src="imageLib.alerm" style="width:36upx;height:36upx;position: absolute;top:22upx;left:0upx;"></image>
						<text style="font-size: 24upx;color:#999;padding-left:6upx;">提示：为了保障您的收益，请务必将邀请码和锁仓激活码一并发给好友</text>
					</view>
				</view>
				<view class="main-title">
					我的收益
				</view>
				<view class="fun-card">
					<view class="fun-card-item">
						<view class="lock-total-box">
							<view class="lock-item-box">
								<view class="lock-item">
									<text class="text-vertical-top">好友数量</text>
									<text class="text-vertical-bottom">8</text>
									<text class="text-vertical-top">一级好友</text>
								</view>
							</view>
							<view class="lock-item-box">
								<view class="lock-item">
									<text class="text-vertical-top">推广收益</text>
									<text class="text-vertical-bottom">888</text>
									<text class="text-vertical-top">一级贡献</text>
								</view>
							</view>
						</view>
					</view>
				</view>
				<view class="section-content" style="padding:0px;padding-top:40upx;">
					<view class="section-subtitle">奖励规则</view>
					<view class="section-part">
						<span class="list-num">1.</span>
						邀请好友</br>邀请好友锁仓，可获得一级好友锁仓分红收益返佣，邀请好友数量无上限。
					</view>
					<view class="section-part">
						<span class="list-num">2.</span>
						锁仓激活码</br>邀请好友时，将你的锁仓激活码赠与他，他参与自主锁仓时，须填写你的锁仓激活码，你才能参与他的收益分红，否则无法获得收益。
					</view>
					<view class="section-part">
						<span class="list-num">3.</span>
						分红比例</br>按照不同时长，不同数量进行阶梯分红。好友锁仓时间越久，数量越多，则你拿到的分红比例越大。具体说明详见下表：
					</view>
				</view>
				<view class="fun-card" style="margin-top:30upx;">
					<view class="fun-card-item">
						<view class="fun-table">
							<view class="fun-table-header trans">锁仓分红返佣说明</view>
							<view class="fun-table-body">
								<view class="fun-table-tr noborder">
									<view class="trans four shadow">好友层级</view>
									<view class="trans four">一个月</view>
									<view class="trans four">三个月</view>
									<view class="trans four">五个月</view>
								</view>
								<view class="fun-table-tr noborder">
									<view class="trans four shadow">一级</view>
									<view class="trans four white">3%</view>
									<view class="trans four white">5%</view>
									<view class="trans four white">8%</view>
								</view>
							</view>
						</view>
					</view>
					<view class="fun-horizen"></view>
					<view class="fun-card-item" style="font-size: 24upx;color:#fff;line-height: 58upx;">
						百分比分别代表：一级好友锁仓收益的占比，如我的一级好友锁仓金额为 1000万枚 Forest，期限 3 个月，收益为4%，则我的返佣=1000万*4%*5%。
					</view>
				</view>
				<view class="main-title" style="padding-top:40upx;">
					邀请记录
				</view>
				<view class="fun-table">
					<view class="fun-table-body">
						<view class="fun-table-tr noborder">
							<view class="trans five">日期</view>
							<view class="trans five">被邀请人 UID</view>
							<view class="trans five">是否填写 激活码</view>
							<view class="trans five">分红币种</view>
							<view class="trans five">分红收益</view>
						</view>
						<view class="fun-table-tr noborder">
							<view class="trans five small">2019/01/22</view>
							<view class="trans five small">100098</view>
							<view class="trans five small">是</view>
							<view class="trans five small">Xdag</view>
							<view class="trans five small">12.8998</view>
						</view>
					</view>
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
				isVip:false,
				imageLib:{
					alerm:'../../static/icons/icon_notification.png'
				}
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			openVip(){
				uni.showModal({
					title:'购买 SVIP 会员',
					content:'您即将购买SVIP会员，我们将从您的钱包中直接扣除199USDT，会员有效期一年。',
					success:res=>{
						console.log(res);
						if(res.confirm){
							
						}else if(res.cancel){
							
						}
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.lock-total-box{
		width:100%;
		display:flex;
		justify-content:space-between;
		padding:20upx 0px;
		.lock-item-vertical{
			width:2upx;
			background:rgba(255,255,255,0.1);
			height:108upx;
		}
		.lock-item-box{
			width:46%;
			display:flex;
			justify-content:space-around;
			flex-wrap:wrap;
			.lock-item-block{
				margin:auto;
				width:160upx;
				border:1px solid rgba(255,255,255,0.5);
				border-radius: 8upx;
				text-align: center;
				font-size: 28upx;
				line-height: 52upx;
				margin-top:20upx;
				color:#c7c7c7;
				display:flex;
				justify-content:space-around;
				flex-wrap:wrap;
			}
			.lock-item{
				width:100%;
				text-align:center;
				text{
					display: block;
				}
			}
		}
	}
	.lockpay-box{
		width:750upx;
		background: #000;
		margin-bottom:30upx;
		.lock-table{
			padding:20upx 40upx;
			table{
				width:100%;
				border:none;
				thead{
					tr{
						th{
							border:none;
							text-align: center;
							line-height: 64upx;
							font-size: 28upx;
							color:#fff;
						}
					}
				}
				tbody{
					tr{
						td{
							border:none;
							text-align: center;
							line-height: 64upx;
							font-size: 28upx;
							color:#c7c7c7;
						}
					}
				}
			}
		}
		.lock-tab{
			border-bottom:2upx solid rgba(255,255,255,0.1);
			display:flex;
			justify-content:space-between;
			.lock-tab-item{
				width:100%;
				text-align:center;
				text{
					font-size:28upx;
					color:#fff;
					line-height:80upx;
					height:80upx;
					display: inline-block;
				}
				&.active text{
					border-bottom:2upx solid #fff;
				}
			}
		}
	}
	.text-vertical-top{
		font-size:28upx;
		color:#fff;
		opacity: 0.5;
	}
	.text-vertical-bottom{
		font-size:48upx;
		color:#fff;
		font-family: 'Montserrat-Light';
		line-height: 100upx;
	}
	.text-horizon-left{
		font-size:28upx;
		color:#fff;
		font-family: 'Montserrat-Bold';
		display: inline-block !important;
		padding:0upx 10upx;
	}
	.text-horizon-right{
		font-size:24upx;
		color:#999;
		font-family: 'Montserrat-Light';
		line-height: 48upx;
		display: inline-block !important;
	}
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
	
</style>
