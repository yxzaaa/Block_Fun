<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="锁仓规则" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container">
			<view class="wallet-banner">
				<image :src="imageLib.banner" />
			</view>
			<view class="section-header">
				<image :src="imageLib.prenote" class="section-icon"></image>
				<text class="section-title">锁仓前提</text>
			</view>
			<view class="section-content">
				<text class="section-subtitle">分红前提：</text>
				<text class="section-describe">
					需要成为SVIP,方能参与锁仓享受分红。SVIP用户享有自主锁仓分红资质，资质定价 199 USDT/年
				</text>
			</view>
			<view class="section-content">
				<text class="section-subtitle">锁仓币种：</text>
				<text class="section-describe">
					参与锁仓的币为Forest/Xdag,则参与分红的币对应着为Forest/Xdag。如下：
				</text>
			</view>
			<view style="width:640upx;margin:30upx 55upx;border:1upx solid #666;border-radius:20upx;padding:24upx 0upx;display: flex;justify-content: center;align-items: center;">
				<view class="ex-box">
					<text style="font-size: 28upx;color:#fff">Forest</text>
					<text style="font-size: 24upx;color:#999">参与锁仓的币</text>
				</view>
				<image :src="imageLib.line" style="width:80upx;height:10upx;"></image>
				<view class="ex-box">
					<text style="font-size: 28upx;color:#fff">Forest</text>
					<text style="font-size: 24upx;color:#999">参与分红的币</text>
				</view>
			</view>
			<view class="section-header">
				<image :src="imageLib.locktype" class="section-icon"></image>
				<text class="section-title">锁仓类型</text>
			</view>
			<view class="section-content">
				<view class="section-subtitle">自主锁仓</view>
				<view class="section-part">
					锁仓采用梯度分红，即按照不同时长，不同数量进行阶梯量化， 锁仓时间越久，数量越多，则拿到的分红比例越大。具体说明详见下表：
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
				<view class="section-subtitle">邀请好友锁仓</view>
				<view class="section-part">
					邀请好友锁仓，可获得一级好友锁仓分红收益返佣，具体说明详见下表：
				</view>
				<view class="fun-table">
					<view class="fun-table-header">锁仓分红返佣说明</view>
					<view class="fun-table-body">
						<view class="fun-table-tr">
							<view class="deep four shadow">好友层级</view>
							<view class="light four">一个月</view>
							<view class="deep four">三个月</view>
							<view class="light four">五个月</view>
						</view>
						<view class="fun-table-tr noborder">
							<view class="deep four shadow">一级</view>
							<view class="light four white">3%</view>
							<view class="deep four white">5%</view>
							<view class="light four white">8%</view>
						</view>
					</view>
				</view>
				<view style="font-size: 22upx; color:#999;padding:20upx 15upx;text-align: center;padding-bottom:40upx;">
					百分比分别代表：一级好友锁仓收益的占比，如我的一级好友锁仓金额为 1000 万枚 Forest，期限 3 个月，收益为 4%，则我的返佣 = 1000 万 × 4% × 5%
				</view>
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
					message:'../../static/icons/message.png',
					union:'../../static/icons/Union.png',
					banner:'../../static/banner2.jpg',
					prenote:'../../static/icons/icon_pre.png',
					locktype:'../../static/icons/icon_type.png',
					line:'../../static/icons/line.png'
				},
				activeTab:0
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
	}
</script>

<style lang="scss" scoped>
	.wallet-banner{
		width:750upx;
		padding:30upx 40upx;
		padding-top:174upx;
		position:relative;
		image{
			width:100%;
			height:520upx;
			display: block;
		}
	}
	.ex-box{
		text-align:center;
		padding:0px 20upx;
		text{
			display: block;
			line-height: 48upx;
		}
	}
</style>
