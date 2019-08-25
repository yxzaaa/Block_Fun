<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="Blockfun" textColor="#fff" :opacity="scroll" layout="left" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container">
			<view class="wallet-banner">
				<img src="static/banner.jpg" alt="">
			</view>
			<view class="button-list">
				<block v-for="(item,index) in buttonList" :key="index">
					<navigator class="button-list-item" url="../shopping/shopping">
						<image :src="item.iconSrc"></image>
						<text>{{item.name}}</text>
					</navigator>
				</block>
			</view>
			<view class="news-box">
				<view class="news-list">
					<image src="../../static/icons/message.png"></image>
					<text>{{message}}</text>
				</view>
				<view class="more-detail">更多</view>
			</view>
			<view class="section-header">
				<text class="section-title">我的钱包</text>
			</view>
			<view class="wallet-list">
				<block v-for="item in walletList" :key="item.walletid">
					<view class="fun-card">
						<view class="fun-card-item">
							<view class="item-horizen">
								<image class="wallet-list-avatar" :src="item.avatar"></image>
								<view class="title-box">
									<text style="font-size: 32upx;color:#fff;">{{item.title}}</text>
									<text style="font-size:24upx;color:#999;">{{item.blockNum}}</text>
								</view>
								<view>
									<image class="button-image" src="../../static/icons/Union.png"/>
								</view>
							</view>
							<view class="item-horizen count-box">
								<text><span>$</span>{{item.total}}</text>
							</view>
							<view class="item-horizen label-line">
								<text><span class="label">数量</span>{{item.count}}</text> 
								<text><span class="label">价格</span>{{item.price}}<span class="kind">{{item.currency}}</span></text> 
							</view>
							<view class="fun-card-buttons">
								<fun-buttton type="text" value="查看账单" />
								<view class="button-group">
									<fun-buttton type="light" value="转账" icon="../../static/icons/zhuanrang-tiny.png" />
									<fun-buttton value="收款" icon="../../static/icons/shoukuan.png" />
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
	import FunButtton from '@/components/fun-button.vue';
	export default{
		components:{
			UniNavBar,
			UniBackground,
			FunButtton
		},
		data(){
			return {
				scroll:0,
				navButtons:{
					search:{
						type:'normal'
					}
				},
				message:"Forest 矿机即将上线，首批抢购名额1000名",
				buttonList:[
					{
						name:'智能锁仓',
						iconSrc:'../../static/icons/suocang.png'
					},
					{
						name:'抵押借贷',
						iconSrc:'../../static/icons/jiedai.png'
					},
					{
						name:'场外交易',
						iconSrc:'../../static/icons/jiaoyi.png'
					},
					{
						name:'信任转让',
						iconSrc:'../../static/icons/zhuanrang.png'
					},
				],
				walletList:[
					{
						walletid:1,
						avatar:'../../static/avatar/fortoken.png',
						title:'Forset Wallet',
						blockNum:'0xEc9…x34e518da',
						total:'8398.58',
						count:'10000',
						price:'0.88',
						currency:'USD'
					},
					{
						walletid:2,
						avatar:'../../static/avatar/fortoken.png',
						title:'Forset Wallet',
						blockNum:'0xEc9…x34e518da',
						total:'8398.58',
						count:'10000',
						price:'0.88',
						currency:'USD'
					},
					{
						walletid:3,
						avatar:'../../static/avatar/fortoken.png',
						title:'Forset Wallet',
						blockNum:'0xEc9…x34e518da',
						total:'8398.58',
						count:'10000',
						price:'0.88',
						currency:'USD'
					},
				]
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
		padding:40upx;
		padding-top:calc(72px + 30upx);
		img{
			width:100%;
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
				font-size: 22upx;
				color:#999;
				max-width: 500upx;
				overflow: hidden;
				text-overflow: ellipsis;
				white-space: nowrap;
			}
		}
		.more-detail{
			color:#666;
			font-size: 22upx;
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
			width:425upx;
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
			text{
				color:#DA53A2;
				font-size: 42upx;
				font-weight: bold;
				span{
					font-size: 32upx;
					display: inline-block;
					padding-right:10upx;
				}
			}
		}
		.label-line{
			padding:15upx 0upx;
			text{
				display: inline-block;
				width:240upx;
				font-size: 24upx;
				color:#c7c7c7;
				span.label{
					color:#999;
					display: inline-block;
					padding-right:20upx;
				}
				span.kind{
					display: inline-block;
					padding-left:10upx;
				}
			}
		}
	}
</style>
