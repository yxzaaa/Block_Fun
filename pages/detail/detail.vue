<template>
	<!-- 商品详情页1 -->
	<view>
		<uni-background />
		<uni-nav-bar 
			:opacity="scroll"
			:buttons="navButtons"
			
			
		/>
		<swiper class="carousel" indicator-dots=true circular=true interval="3000" duration="700">
			<swiper-item v-for="(item,index) in data.imgList" :key="index">
				<view class="image-wrapper">
					<image
						:src="item.src" 
						:class="item.loaded" 
						mode="aspectFill"
						@load="imageOnLoad('imgList', index)" 
						style="width:100%;height:738upx;"
					></image>
				</view>
			</swiper-item>
		</swiper>
		<!-- <view class="scroll-view-wrapper">
			<scroll-view class="episode-panel" :class="{Skeleton:!loaded}" scroll-x>
				<view v-for="(item, index) in data.episodeList" :key="index"
					:class="{current: currentEpd===item}"
					@click="changeEpd(index)"
				>
					{{item}}
				</view>
			</scroll-view>
		</view> -->
		<view class="info">
			<view class="title">
				<text :class="{Skeleton:!loaded}" style="margin-top:40upx;">
					<span style="font-size:30upx;margin-right:10upx;font-family:'Montserrat-Bold';">{{data.symbol}}</span>
					<span style="font-size:40upx;font-family:'Montserrat-Bold';">{{data.money.split('.')[0]}}</span>
					<span style="font-size: 30upx;font-family:'Montserrat-Bold';">{{data.money.split('.')[1]?'.' + data.money.split('.')[1]:''}}</span>
				</text>
				
				<text :class="{Skeleton:!loaded}" style="color:#999999;font-size:24upx;margin-top:16upx;">{{data.consume}} {{data.amount}}</text>
				<text :class="{Skeleton:!loaded}" style="background:#DA53A2;height:32upx;width:64upx;text-align: center;font-size:24upx;color:#fff;margin-top:16upx;">{{data.character}}</text>
				<text :class="{Skeleton:!loaded}" style="color:#fff;font-size: 32upx;margin-top:16upx;">{{data.title}}</text>
				<text :class="{Skeleton:!loaded}" style="color:#999999;font-size: 24upx;margin-top:16upx;">{{data.content}}</text>
			</view>
		</view>
		<!-- <view class="actions">
			<text class="yticon icon-fenxiang2" @click="share"></text>
			<text class="yticon icon-Group-"></text>
			<text class="yticon icon-shoucang" :class="{active: data.favorite}" @click="favorite"></text>
		</view> -->

		<!-- 相关推荐-->
		<view class="guess">
			<view class="section-tit">相关推荐</view>
			<view class="guess-list">
				<view 
					v-for="(item, index) in data.guessList" :key="index"
					class="guess-item"
					style="padding-top:16upx;"
				>
				<!-- 引入图片 -->
					<view class="image-wrapper">
						<image 
							:src="item.src" 
							:class="item.loaded" 
							mode="aspectFill"
							@load="imageOnLoad('guessList', index)" 
						></image>
					</view>
					<!-- 图片描述 -->
					<view class="guess-content" style="margin-left:20upx;margin-top:0;">
						<text class='title clamp' :class="{Skeleton:!loaded}" style="font-size: 30upx;color:#fff;">{{item.title}}</text>
						<text class="clamp" :class="{Skeleton:!loaded}" style="font-size: 30upx;color:#fff;margin-top:10upx;">{{item.title2}}</text>
						<text class="clamp" :class="{Skeleton:!loaded}" style="font-size:30upx;color:#999999;margin-top:14upx;">{{item.consume}} {{item.amount}}</text>
						<text class="clamp" :class="{Skeleton:!loaded}" style="margin-top:14upx;color:#DA53A2;font-family:'Montserrat-Bold';">
							<span style="font-size:24upx;margin-right:8upx;">{{item.symbol}}</span>
							<span>{{item.price.split('.')[0]}}</span>
							<span style="font-size:24upx;">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
						</text>
					</view>
				</view>
			</view>
		</view>
		<!-- 评论 -->
		<!-- <view class="evalution">
			<view class="section-tit">评论</view>
			<view class="eva-list" :class="{Skeleton:!loaded}">
				<view  v-for="(item, index) in data.evaList" :key="index"
					class="eva-item"
				>
					<image :src="item.src" mode="aspectFill"></image>
					<view class="eva-right">
						<text>{{item.nickname}}</text>
						<text>{{item.time}}</text>
						<view class="zan-box">
							<text>{{item.zan}}</text>
							<text class="yticon icon-shoucang"></text>
						</view>
						<text class="content">{{item.content}}</text>
					</view>
				</view>
			</view>
		</view> -->
		<!-- 分享 -->
		<share 
			ref="share" 
			:contentHeight="580"
			:shareList="shareList"
		></share>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import share from '@/components/share';
	export default {
		components: {
			share,
			UniNavBar,
			UniBackground,
		},
		data() {
			return {
				scroll:0,
				loaded: false,
				currentEpd: 1,
				data: {
					guessList: [{},{},{},{}] 
				},
				shareList: [],
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
		async onLoad(){
			let detailData = await this.$api.json('detailData');
			let shareList = await this.$api.json('shareList');
			this.loaded = true;
			this.data = detailData;
			this.shareList = shareList;
			uni.setNavigationBarTitle({
				title: detailData.title
			})
		},
		methods:{
			imageOnLoad(key,index){
				this.$set(this.data[key][index], 'loaded', 'loaded');
			},
			changeEpd(index){
				let list = this.data.episodeList;
				let epd = list[index];
				this.$api.msg(`切换到第${epd}项`);
				this.currentEpd = epd;
			},
			//分享
			share(){
				this.$refs.share.toggleMask();	
			},
			//收藏
			favorite(){
				this.data.favorite = !this.data.favorite;
			}
		},
		//处理遮罩层物理返回键
		onBackPress(){
			if(this.$refs.share.show){
				this.$refs.share.toggleMask();
				return true;
			}
		}
	}
</script>

<style lang="scss">
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
		padding: 10upx 40upx;
		// background: #fff;

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
				&.Skeleton{
					width:220upx;
				}
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
			&.active{
				color: #ff4443;
			}
			&:nth-child(2) {
				font-size: 50upx;
			}
		}
	}

	.section-tit {
		font-size: $font-base+2upx;
		color: #fff;
		margin-bottom: 30upx;
	}

	.guess {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 30upx 40upx 10upx;
		margin-top: 16upx;
		
		
	}

	.guess-list {
		// display: flex;
		// flex-wrap: wrap;
		width: 100%;
	}
	.guess-item {
		display: flex;
		overflow: hidden;
		min-width: 40%;
		margin-right: 26upx;
		padding-bottom: 40upx;
	
		.image-wrapper{
			width: 200upx;
			height: 200upx;
			border-radius: 10upx;
		}
	
		.guess-content {
			color:#999999;
			// font-size: $font-sm;
			// color: $font-color-light;
			// &.Skeleton{
			// 	width: 180upx;
			// 	&.title{
			// 		width: 140upx;
			// 	}
			// }
			// &.title{
			// 	font-size: $font-base+2upx;
			// 	color: $font-color-dark;
			// 	margin-top:16upx;
			// 	margin-bottom: 8upx;
			// }
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
</style>
