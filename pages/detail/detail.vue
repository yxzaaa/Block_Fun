<template>
	<!-- 商品详情页1 -->
	<view>
		<uni-background />
		<uni-nav-bar 
			:opacity="scroll"
			:buttons="navButtons"			
		/>
		<view class="app-container fixbutton">
			<swiper class="carousel" indicator-dots=true circular=true interval="3000" duration="700" indicator-active-color="#DA53A2">
				<swiper-item v-for="(item,index) in imgList" :key="index">
					<view class="image-wrapper">
						<image
							:src="item.src" 
							mode="aspectFill"
							style="width:100%;height:738upx;"
						></image>
					</view>
				</swiper-item>
			</swiper>
			<view class="info">
				<view class="title">
					<text style="margin-top:40upx;">
						<span style="font-size:30upx;margin-right:6upx;font-family:'Montserrat-Bold';">{{symbol}}</span>
						<span style="font-size:40upx;font-family:'Montserrat-Bold';">{{money.split('.')[0]}}</span>
						<span style="font-size: 30upx;font-family:'Montserrat-Bold';">{{money.split('.')[1]?'.' + money.split('.')[1]:''}}</span>
					</text>
					
					<text style="color:#999999;font-size:24upx;margin-top:16upx;">{{consume}} {{amount}}</text>
					<text style="background:#DA53A2;height:32upx;width:64upx;text-align: center;font-size:24upx;color:#fff;margin-top:16upx;">{{character}}</text>
					<text style="color:#fff;font-size: 32upx;margin-top:16upx;">{{title}}</text>
					<text style="color:#999999;font-size: 24upx;margin-top:16upx;width:670upx;height:322upx;line-height:44upx;">{{content}}</text>
				</view>
			</view>
			
			<!-- 相关推荐-->
			<view class="guess">
				<view class="section-tit">相关推荐</view>
				<view class="guess-list">
					<navigator
						v-for="(item, index) in guessList" :key="index"
						class="guess-item"
						url="../detail/detail"
					>
					<!-- 引入图片 -->
						<view class="image-wrapper">
							<image 
								:src="item.src" 
								mode="aspectFill"
							></image>
						</view>
						<!-- 图片描述 -->
						<view class="guess-content" style="margin-left:20upx;margin-top:0;">
							<span class='title clamp' style="font-size:28upx;color:#fff;white-space: normal;width:448upx;height:88upx;">{{item.title.substring(0,40)+' ...'}}</span>
							<span class="clamp" style="font-size:24upx;color:#999999;margin-top:12upx;">{{item.consume}} {{item.amount}}</span>
							<span class="clamp" style="margin-top:12upx;color:#DA53A2;font-family:'Montserrat-Bold';">
								<span style="font-size:24upx;margin-right:8upx;font-family:'Montserrat-Bold';">{{item.symbol}}</span>
								<span style="font-family:'Montserrat-Bold';">{{item.price.split('.')[0]}}</span>
								<span style="font-size:24upx;font-family:'Montserrat-Bold';">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
							</span>
							
						</view>
					</navigator>
				</view>
			</view>
			
			<!-- 底部按钮 -->
			<view class="fixed-buttons" style="display: flex;justify-content: space-between;align-items: center;">
				<view style="width:66upx;height:44upx;padding-left:30upx;" class="button-group">
					<image src="../../static/bg/listen.png" style="width:36upx;height:44upx;"></image>
				</view>
				
				<view class="button-group" style="width:500upx;">
					<fun-button value="加入购物车" type="light" width="240upx" large></fun-button>
					<fun-button value="立即购买" width="240upx" large url="../order-management/order-management"></fun-button>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import FunButton from '@/components/fun-button.vue';
	import share from '@/components/share';
	export default {
		components: {
			share,
			UniNavBar,
			UniBackground,
			FunButton
		},
		data() {
			return {
				scroll:0,
				loaded: false,
				currentEpd: 1,
				symbol:"￥",
				money: '6044.13',
				consume: '消耗积分',
				amount:'4000',
				favorite: true,
				character:"日用",
				title:"日本ANESSA安耐晒进口金平安热沙防晒乳防水隔离SPF50+60ml",
				content:"防晒霜，是指添加了能阻隔或吸收紫外线的防晒剂来达到防治肌肤被晒黑、晒伤的化妆品、根据防晒原理可将防晒霜分为物理防晒霜、化学防晒霜、防晒霜需要根据具体的对象来选择不同SPF或PA值的产品。以达到防晒的目的。防晒霜的作用原理是将皮肤与紫外线隔离开来。防晒乳跟防晒霜，主要区别在于物理性状，霜剂一般的含水量在60%左右，看上去比较“稠”，呈膏状；而乳液，含水量在70%以上，看上去比较稀，有流动性。",
				imgList: [
					{
						src: '../../static/bg/detail1.png'
					},
					{
						src: 'http://img.pconline.com.cn/images/upload/upc/tx/itbbs/1309/06/c4/25310541_1378426131583.jpg'
					},
					{
						src: 'http://img.pconline.com.cn/images/upload/upc/tx/photoblog/1610/26/c4/28926240_1477451226577_mthumb.jpg'
					},
					{
						src: 'http://picture.ik123.com/uploads/allimg/190219/12-1Z219105139.jpg'
					}, 
				],
				guessList: [{
						src: '../../static/bg/iphonex.png',
						src1:'../../static/bg/checkbox.png',
						title: 'Apple iPhone X (A1865) 256GB 深空灰色 移动联通电信4G手机',
						consume:'消耗积分',
						amount:'4000',
						symbol:"￥",
						price:'6444.13',
						number:'0'
					},
					{
						src: '../../static/bg/p30.png',
						src1:'../../static/bg/check.png',
						title: '华为P30 (A1865) 256GB 深空灰色 移动联通电信4G手机',
						consume:'消耗积分',
						amount:'4000',
						symbol:"￥",
						price:'4999.21',
						number:'0',
					},
					{
						src: '../../static/bg/apple.png',
						src1:'../../static/bg/checkbox.png',
						title: 'Apple iPhone X(A1865) 256GB 深空灰色 移动联通电信4G手机',
						consume:'消耗积分',
						amount:'4000',
						symbol:"￥",
						price:'4999.21',
						number:'0',
					},
				],
				navButtons:{
					back:{
						type:'circle',
						text:'取消'
					},
					share:{
						type:'circle'
					},
					love:{
						type:'circle',
						
					},
					cart:{
						type:'circle',
						url:"../cart1/cart1"
					},
					// textbtn:{
					// 	text:'取消'
					// }
				}
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
		},
		methods:{
			
		},
	}
</script>

<style lang="scss" scoped>
	// page{
	// 	background: $page-color-base;
	// }

	.carousel {
		height:738upx;
		.image-wrapper{
			display: flex;
			justify-content: center;
			align-content: center;
			width: 100%;
			height: 100%;
			overflow: hidden;

			image {
				width: 100%;
				height: 100%;
			}
		}
	}
	.scroll-view-wrapper{
		display:flex;
		align-items:center;
		height: 90upx;
		padding: 20upx 0 20upx 40upx;
		
	}
	.episode-panel {
		white-space: nowrap;
		width: 100%;
		view {
			display: inline-block;
			margin-right: 30upx;
			width: 56upx;
			font-size: $font-lg;
			color: $font-color-base;
			&.current{
				color: #07a7a7;
			}
		}
	}

	.info {
		display: flex;
		align-items: center;
		padding: 10upx 38upx 72upx;
		border-bottom:1px solid rgba(255,255,255,0.1);	

		.title {
			flex: 1;
			display: flex;
			flex-direction: column;
			font-size: $font-lg + 4upx;
			color: #DA53A2;

			text:last-child {
				font-size: $font-sm;
				color: $font-color-light;
				margin-top: 4upx;
			}
		} 
		
	}

	.actions {
		padding: 10upx 28upx;
		// background: #fff;

		.yticon {
			font-size: 46upx;
			color: $font-color-base;
			padding: 10upx 12upx;
			
		}
	}

	.section-tit {
		width:670upx;
		font-size: 32upx;
		color: #fff;
		margin-bottom: 30upx;
	}

	.guess {
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: center;
		padding: 30upx 40upx 10upx;
		margin-top: 16upx;
		
		
	}

	.guess-list {
		width: 100%;
	}
	.guess-item {
		display: flex;
		padding-bottom:40upx;
	
		.image-wrapper{
			width: 200upx;
			height: 200upx;
			border-radius: 10upx;
			image{
				width:200upx;
				height:200upx;
			}
		}
	
		.guess-content {
			color:#999999;
			height:200upx;
		}
	}
	.evalution{
		display:flex;
		flex-direction:column;
		// background: #fff;
		margin-top: 16upx;
		padding: 40upx 0;
	}

	.eva-item{
		display:flex;
		padding: 20upx 40upx;
		image{
			width: 60upx;
			height: 60upx;
			// border-radius: 50px;
			flex-shrink: 0;
			margin-right: 24upx;
		}
	}
	.eva-right{
		display:flex;
		flex-direction:column;
		flex: 1;
		font-size: $font-sm + 2upx;
		color: $font-color-light;
		position:relative;
		.zan-box{
			display:flex;
			align-items:base-line;
			position:absolute;
			top: 10upx;
			right: 10upx;
			.yticon{
				margin-left: 8upx; 
			}
		}
		.content{
			font-size: $font-base;
			color: #333;
			padding-top:20upx;
		}
	}
	.bottombar{
		width:100%;
		height:120upx;
		position:fixed;
		bottom:0;
		left:0;
		background:#2F282B;
	}
</style>
