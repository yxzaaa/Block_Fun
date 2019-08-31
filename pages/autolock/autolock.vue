<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="自主锁仓" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view style="padding:0upx 40upx;padding-bottom:30upx;">
				<view class="fun-card">
					<view class="fun-card-item" v-if="!isVip">
						<view class="main-title">您还不具备锁仓资格</view>
						<view class="section-content" style="padding:5upx 0upx;">
							<text class="section-subtitle">资格兑换：</text>
							<text class="section-describe">
								自主锁仓分红，是SVIP会员的专属权益，普通会员无法享受此权益；
							</text>
						</view>
						<view class="section-content" style="padding:5upx 0upx;">
							<text class="section-subtitle">SVIP会员权益说明：</text>
							<text class="section-describe">
								钱包手续费分红（总收益的30%）；自主锁仓资格；邀请锁仓返佣；OTC挂单资格；金牌理财资格（私募）；
							</text>
						</view>
						<view class="gold-button" @click="openVip">
							<image :src="imageLib.goldbg"></image>
							<text style="font-size: 24upx;color:#26262B;position: relative;z-index: 2;">199 USTD/年 </text>
							<text style="font-size: 32upx;color:#26262B;position: relative;z-index: 2;padding-left:10upx;"> · 成为 SVIP</text>
						</view>
					</view>
					<view class="fun-card-item" v-else>
						<view class="main-title gold">您是尊贵的SVIP会员，享有锁仓特权</view>
						<view class="section-content" style="padding:5upx 0upx;">
							<text class="section-subtitle">资格兑换：</text>
							<text class="section-describe">
								自主锁仓分红，是SVIP会员的专属权益，普通会员无法享受此权益；
							</text>
						</view>
						<view class="section-content" style="padding:5upx 0upx;">
							<text class="section-subtitle">SVIP会员权益说明：</text>
							<text class="section-describe">
								钱包手续费分红（总收益的30%）；自主锁仓资格；邀请锁仓返佣；OTC挂单资格；金牌理财资格（私募）；
							</text>
						</view>
					</view>
				</view>
				<view class="fun-card" style="margin-top:40upx;">
					<view class="fun-card-item">
						<view class="form-item">
							<view class="form-label">填写锁仓激活码<text class="des-item">选填</text></view>
							<view class="form-value-box" style="padding-bottom:20upx;">
								<view class="form-input-box">
									<input class="form-input-field" placeholder="请填写好友赠予的的激活码"/>
								</view>
							</view>
							<view style="font-size: 24upx;color:#fff;padding-bottom:30upx;">填写额外奖励 100 枚 Xdag</view>
						</view>
						<view class="form-item" style="margin-bottom:40upx;">
							<view class="form-label" style="margin-bottom:20upx;">锁仓币种</view>
							<view class="radio-box">
								<text style="width:50%;" class="active">Forest</text>
								<text style="width:50%;">Xdag</text>
							</view>
						</view>
						<view class="form-item">
							<view class="form-label">锁仓数量</view>
							<view class="form-value-box" style="padding-bottom:20upx;">
								<view class="form-input-box">
									<input class="form-input-field" placeholder="钱包余额 10000 个"/>
									<view class="form-input-btns">
										<text>全部</text>
									</view>
								</view>
							</view>
							<view style="font-size: 24upx;color:#999;padding-bottom:30upx;">
								<text>100 个起</text>
								<text style="float:right;">参与后，T+1日开始计算分红</text>
							</view>
						</view>
						<view class="form-item" style="padding-bottom:0px;">
							<view class="form-label" style="margin-bottom:20upx;">锁仓时长</view>
							<view class="radio-box">
								<text style="width:33.3%;" class="active">30天</text>
								<text style="width:33.3%;">90天</text>
								<text style="width:33.3%;">150天</text>
							</view>
						</view>
					</view>
					<view class="fun-horizen"></view>
					<view class="fun-card-item">
						<view class="form-item" style="padding:0px;">
							<view class="input-field" style="text-align: center;padding:20upx 0upx;border-radius: 10upx;">
								<text style="display:block;font-size: 24upx;color:#fff;opacity: 0.5;width:100%;">预计每日 Forest 分红</text>
								<text style="display:block;font-size: 62upx;color:#fff;line-height: 76upx;width:100%;font-family: 'Montserrat-Bold';">23.1234</text>
							</view>
						</view>
					</view>
				</view>
				<view style="margin:30upx 0upx">
					<fun-button value="确认锁仓" block width="670upx" large></fun-button>
					<view style="display: flex;align-items: center;justify-content: center;padding-top:20upx;">
						<image :src="imageLib.checked" style="width:24upx;height:24upx;margin-right:10upx;"></image>
						<text  style="font-size:24upx;color:#999">我同意《锁仓分红服务协议》</text>
					</view>
				</view>
				<view class="section-content" style="padding:10upx 0upx;">
					<view class="section-subtitle">规则说明</view>
					<view class="section-part">
						<span class="list-num">1.</span>
						锁仓币种：参与锁仓的币为Forest/Xdag，则参与分红的币对应着为Forest/Xdag。如参与锁仓的币是Forest，则参与分红的币也是Forest。
					</view>
					<view class="section-part">
						<span class="list-num">2.</span>
						分红前提：需要成为SVIP会员，方能参与锁仓享受分红。SVIP用户享有自主锁仓分红资质，资质定价199USDT/年。
					</view>
					<view class="section-part">
						<span class="list-num">3.</span>
						分红机制：锁仓采用梯度分红，即按照不同时长，不同数量进行阶梯量化。锁仓时间越久，数量越多，则拿到的分红比例越大。具体说明详见下表：
					</view>
					<view class="fun-table">
						<view class="fun-table-header">梯度分红说明</view>
						<view class="fun-table-body">
							<view class="fun-table-tr">
								<view class="deep five shadow">锁仓数量</view>
								<view class="light five small">>=8000</view>
								<view class="deep five small">>=80000</view>
								<view class="light five small">>=800000</view>
								<view class="deep five small">>=8000000</view>
							</view>
							<view class="fun-table-tr">
								<view class="deep five shadow">锁仓1个月</view>
								<view class="light five white">0.3%</view>
								<view class="deep five white">0.5%</view>
								<view class="light five white">0.8%</view>
								<view class="deep five white">1%</view>
							</view>
							<view class="fun-table-tr">
								<view class="deep five shadow">锁仓3个月</view>
								<view class="light five white">1%</view>
								<view class="deep five white">1.6%</view>
								<view class="light five white">2.8%</view>
								<view class="deep five white">4%</view>
							</view>
							<view class="fun-table-tr noborder">
								<view class="deep five shadow">锁仓5个月</view>
								<view class="light five white">1.5%</view>
								<view class="deep five white">3.5%</view>
								<view class="light five white">6%</view>
								<view class="deep five white">10%</view>
							</view>
						</view>
					</view>
					<view style="font-size: 22upx; color:#999;padding:20upx 0upx;padding-left:20upx;">
						锁仓到期后，可开启新一轮锁仓。每重启一轮，分红比增加 0.1%
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
					goldbg:'../../static/gold_btn.jpg',
					checked:'../../static/icons/checked.png'
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
	.main-title{
		font-size:36upx;
		color:#fff;
		text-align: center;
		line-height: 64upx;
		font-weight:bolder;
		padding-bottom:10upx;
		&.gold{
			color:#CCB382;
		}
	}
	.gold-button{
		width:100%;
		border-radius: 10upx;
		line-height: 80upx;
		position:relative;
		overflow:hidden;
		margin-top:20upx;
		text-align:center;
		image{
			position:absolute;
			top:0px;
			left:0px;
			width:100%;
			height:100%;
			z-index:0;
		}
		text{
			font-weight: bold;
		}
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
