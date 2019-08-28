<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="账单" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="horizon-tab">
				<horizon-tab :tabs="navTabs" padding="20"/>
			</view>
			<view class="horizon-list">
				<block v-for="(item,index) in xdogList" :key="item.id">
					<navigator class="horizon-list-item" :url="'../xdogdetail/xdogdetail?id='+item.id">
						<view class="avatar-item">
							<image :src="item.avatar"></image>
						</view>
						<view class="left-item">
							<text class="left-item-title">{{item.title}}</text>
							<text class="left-item-date">{{item.date}}</text>
						</view>
						<view class="center-item">
							<text>{{item.symbol}}</text>
						</view>
						<view class="right-item">
							<view v-if="item.status == '!'" class="pre-image">
								<image :src="imageLib.downlock"></image>
							</view>
							<span class="right-item-text" :style="{color:item.status == '+'?'#DA53A2':item.status == '-'?'#56CCF2':'#F2C94C'}">
								<span>{{item.status}}</span>
								{{item.values}}
							</span>
							<image :src="imageLib.more"></image>
						</view>
					</navigator>
				</block>
			</view>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import HorizonTab from '@/components/horizon-tab.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			HorizonTab
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
				imageLib:{
					more:'../../static/icons/more.png',
					downlock:'../../static/icons/downlock.png'
				},
				navTabs:[
					{
						id:1,
						text:'全部'
					},
					{
						id:2,
						text:'推广分红'
					},
					{
						id:3,
						text:'锁仓分红'
					},
					{
						id:4,
						text:'锁仓明细'
					},
					{
						id:5,
						text:'USTD支付'
					},
				],
				xdogList:[
					{
						id:1,
						avatar:'../../static/icons/icon_fenhong.png',
						title:'自主锁仓分红',
						date:'2019/02/04 01:13',
						status:'+',
						symbol:'Forest',
						values:'88.65'
					},
					{
						id:2,
						avatar:'../../static/icons/icon_goumaikuangji.png',
						title:'SVIP资格购买',
						date:'2019/02/04 01:13',
						status:'-',
						symbol:'USTD',
						values:'88.65'
					},
					{
						id:3,
						avatar:'../../static/icons/icon_suocang.png',
						title:'参与自主锁仓',
						date:'2019/02/04 01:13',
						status:'!',
						symbol:'Forest',
						values:'88.65'
					},
				]
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
	}
</script>

<style lang="scss">
	.horizon-list{
		padding:40upx 0upx;
		.horizon-list-item{
			padding:20upx 40upx;
			display: flex;
			justify-content: space-between;
			align-items: center;
			.avatar-item{
				width:56upx;
				margin-right:10upx;
				height:90upx;
				image{
					width:56upx;
					height:56upx;
				}
			}
			.center-item{
				width:100upx;
				font-size: 26upx;
				color:#fff;
				text{
					font-family:'Montserrat-Bold';
				}
			}
			.left-item{
				width:300upx;
				.left-item-title{
					display: block;
					color:#fff;
					font-size: 32upx;
					line-height: 52upx;
					overflow:hidden;
					text-overflow:ellipsis;
					white-space:nowrap;
					span{
						font-family:'Montserrat-Bold';
					}
				}
				.left-item-date{
					display: block;
					color:#999;
					font-size: 24upx;
					line-height: 52upx;
					font-family:'Montserrat-Light';
				}
			}
			.right-item{
				.pre-image{
					image{
						width:28upx;
						height:28upx;
						margin-right:10upx;
					}
				}
				width:300upx;
				display: flex;
				justify-content: flex-end;
				align-items: center;
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
	}
</style>
