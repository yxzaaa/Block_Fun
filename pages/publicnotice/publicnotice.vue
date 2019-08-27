<template>
	<scroll-view class="container">
		<uni-background />
		<uni-nav-bar title="公告" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="notice-head">
				<text style="font-size: 40upx;font-family:'Montserrat-Light';">2019/01/12</text>
				<text>星期二</text>
			</view>
			<view class="notice-list">
				<block v-for="(item,index) in notices" :key="item.id">
					<view class="notice-item">
						<view class="left-line">
							<image :src="imageLib.ellipse"></image>
							<view class="bottom-line" v-if="index !== notices.length-1"></view>
						</view>
						<view class="right-box">
							<text style="color:#fff;font-size: 30upx;">{{item.title}}</text>
							<text>{{item.date}}</text>
							<text>亲爱的社区用户：</text>
							<text>{{item.describe}}</text>
							<navigator style="color:#DA53A2;font-size:28upx;margin-top:20upx;margin-bottom: 40upx;display: inline-block;">查看详情</navigator>
						</view>
					</view>
				</block>
			</view>
		</view>
	</scroll-view>
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
				imageLib:{
					ellipse:'../../static/icons/Ellipse.png'
				},
				notices:[
					{
						id:1,
						title:'Block Fun将支持钱包转账功能',
						date:'18:08',
						describe:'Forest 主网已于 2019/1/24上线。Block Fun将支持钱包转账功能Forest 主网已于 2019/1/24上线。Block Fun将支持钱包转账功能Forest 主网已于 2019/1/24上线。Block Fun将支持钱包转账功能'
					},
					{
						id:2,
						title:'Block Fun将支持钱包转账功能',
						date:'18:08',
						describe:'Forest 主网已于 2019/1/24上线。Block Fun将支持钱包转账功能'
					},
					{
						id:3,
						title:'Block Fun将支持钱包转账功能',
						date:'18:08',
						describe:'Forest 主网已于 2019/1/24上线。Block Fun将支持钱包转账功能'
					},
				]
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
	}
</script>

<style lang="scss" scoped>
	.notice-head{
		width:670upx;
		padding:40upx 0upx;
		padding-top:10px;
		margin:0upx 40upx;
		display:flex;
		justify-content:space-between;
		border-bottom:1px solid rgba(255,255,255,.1);
		text{
			font-size:32upx;
			color:#fff;
		}
	}
	.notice-list{
		width:750upx;
		padding:60upx 40upx;
		.notice-item{
			width:100%;
			height:auto;
			display: flex;
			justify-content: flex-start;
			.left-line{
				width:26upx;
				// height:100%;
				min-height:340upx;
				image{
					width:26upx;
					height:26upx;
					display: block;
				}
				.bottom-line{
					width:5upx;
					background: rgba(255,255,255,0.2);
					height:calc(100% - 26upx);
					margin:auto;
				}
			}
			.right-box{
				width:calc(100% - 26upx);
				padding:0upx 20upx;
				position:relative;
				top:-12upx;
				text{
					font-size: 24upx;
					line-height: 48upx;
					color:#999;
					display: block;
				}
			}
		}
	}
</style>
