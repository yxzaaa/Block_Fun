<template>
	<view class="container">
		<uni-background/>
		<uni-nav-bar title="Blockfun" textColor="#fff" :opacity="scroll" layout="left" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container">
			<view class="wallet-banner">
				<image :src="imageLib.banner" alt="" />
			</view>
			<view class="button-list">
				<block v-for="(item,index) in buttonList" :key="index">
					<navigator class="button-list-item" :url="item.link">
						<image :src="item.iconSrc"></image>
						<text>{{item.name}}</text>
					</navigator>
				</block>
			</view>
			<view class="news-box">
				<view class="news-list">
					<image :src="imageLib.message"></image>
					<text>{{message}}</text>
				</view>
				<navigator class="more-detail" url="../publicnotice/publicnotice">更多</navigator>
			</view>
			<view class="section-header">
				<text class="section-title">我的钱包</text>
			</view>
			<view class="wallet-list">
				<block v-for="(item,index) in walletList" :key="index">
					<view class="fun-card">
						<view class="fun-card-item">
							<view class="item-horizen">
								<image class="wallet-list-avatar" :src="imageLib.avatar"></image>
								<view class="title-box">
									<text style="font-size:32upx;color:#fff;font-family:'Montserrat-Bold';">{{item.coin}}</text>
									<text style="font-size:24upx;color:#999;font-family:'Montserrat-Bold';overflow: hidden;width:300upx;text-overflow: ellipsis;white-space: nowrap;">{{item.address}}</text>
								</view>
								<view>
									<image class="button-image" :src="imageLib.union"/>
								</view>
							</view>
							<view class="item-horizen count-box">
								<span class="label-box"><span>￥</span>{{getNum(item.total_price)}}</span>
							</view>
							<view class="item-horizen label-line">
								<span class="label-box"><span class="label">数量</span>{{getNum(item.balance)}}</span> 
								<span class="label-box"><span class="label">价格</span>{{getNum(item.unit_price)}} USD</span> 
							</view>
							<view class="fun-card-buttons">
								<fun-button type="text" value="查看账单" :url="'../xdogwallet/xdogwallet?coin='+item.coin" />
								<view class="button-group" style="width:340upx;">
									<fun-button @handle="goTransPay(item.coin,item.total_price)" type="light" value="转账" icon="/static/icons/zhuanrang-tiny.png" />
									<fun-button @handle="goSavePay(item.coin)" value="收款" icon="/static/icons/shoukuan.png" />
								</view>
							</view>
						</view>
					</view>
				</block>
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
					search:{
						type:'normal'
					}
				},
				imageLib:{
					message:'../../static/icons/message.png',
					union:'../../static/icons/Union.png',
					banner:'../../static/banner.jpg',
					avatar:'../../static/avatar/fortoken.png'
				},
				message:"Forest 矿机即将上线，首批抢购名额1000名",
				currType:1,
				buttonList:[
					{
						name:'智能锁仓',
						iconSrc:'../../static/icons/suocang.png',
						link:'../lockposition/lockposition'
					},
					{
						name:'抵押借贷',
						iconSrc:'../../static/icons/jiedai.png',
						link:'../pledge-debit/pledge-debit'
					},
					{
						name:'场外交易',
						iconSrc:'../../static/icons/jiaoyi.png',
						link:'../transout/transout'
					},
					{
						name:'信任转让',
						iconSrc:'../../static/icons/zhuanrang.png',
						link:'../assignment/assignment'
					},
				],
				walletList:[]
			}
		},
		onLoad(){
			//获取钱包列表
			uni.showLoading({
				title:'钱包加载中...'
			})
			this.$http({
				url:'/v1/main/users/account-info',
				data:{
					type:this.currType
				},
				success:res=>{
					uni.hideLoading();
					if(res.code == 200){
						this.walletList = res.data;
					}
				}
			})
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onPullDownRefresh(){
			// console.log('aaa');
			// uni.vibrateShort({
			//     success: function () {
			//         console.log('success');
			//     }
			// });
		},
		methods:{
			getNum(num){
				return (parseFloat(num)).toFixed(2);
			},
			//去转账
			goTransPay(coin,total){
				console.log(total);
				uni.navigateTo({
					url:'../transaccount/transaccount?coin='+coin+'&total='+total
				})
			},
			//去收款
			goSavePay(coin){
				uni.navigateTo({
					url:'../saveaccount/saveaccount?coin='+coin
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.wallet-banner{
		width:750upx;
		padding:40upx;
		padding-top:174upx;
		image{
			width:100%;
			height:520upx;
		}
	}
	.button-list{
		display: flex;
		justify-content: space-between;
		padding:0px 20upx;
		.button-list-item{
			width:25%;
			display:flex;
			justify-content:center;
			align-items:center;
			flex-wrap:wrap;
			image{
				width:72upx;
				height:72upx;
			}
			text{
				text-align: center;
				width:100%;
				color:#fff;
				font-size: 24upx;
				line-height: 56upx;
			}
		}
	}
	.news-box{
		width:750upx;
		padding:40upx;
		padding-top:50upx;
		padding-bottom:20upx;
		display: flex;
		justify-content: space-between;
		.news-list{
			display:flex;
			align-items:center;
			image{
				width:36upx;
				height:36upx;
				margin-right:15upx;
			}
			text{
				font-size: 24upx;
				color:#999;
				max-width: 500upx;
				overflow: hidden;
				text-overflow: ellipsis;
				white-space: nowrap;
			}
		}
		.more-detail{
			color:#666;
			font-size: 24upx;
			line-height: 40upx;
		}
	}
	.wallet-list{
		padding:0px 40upx;
		padding-bottom:20upx;
		.fun-card{
			margin-bottom:20upx;
		}
		.title-box{
			width:420upx;
			padding:0px 30upx;
			text{
				display: block;
				width:100%;
			}
		}
		.wallet-list-avatar{
			width:80upx;
			height:80upx;
		}
		.count-box{
			padding:10upx 0upx;
			padding-top:30upx;
			.label-box{
				color:#DA53A2;
				font-size: 42upx;
				font-family:'Montserrat-Bold';
				span{
					color:#DA53A2;
					font-size: 32upx;
					display: inline-block;
					padding-right:10upx;
					font-family:'Montserrat-Bold';
				}
			}
		}
		.label-line{
			padding:15upx 0upx;
			.label-box{
				display: inline-block;
				width:240upx;
				font-size: 24upx;
				color:#c7c7c7;
				.label{
					color:#999;
					display: inline-block;
					padding-right:20upx;
				}
				.kind{
					display: inline-block;
					padding-left:10upx;
				}
			}
		}
	}
</style>
