<template>
	<!-- 商品详情页1 -->
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			:opacity="scroll"
			title="游戏"
			textColor="#fff"
		/>
		<view class="app-container full">
			<swiper class="carousel" indicator-dots=true circular=true interval="3000" duration="700">
				<swiper-item v-for="(item,index) in data.imgList" :key="index">
					<view class="image-wrapper">
						<image
							:src="item.src" 
							:class="item.loaded" 
							mode="aspectFill"
							@load="imageOnLoad('imgList', index)" 
							style="width:670upx;height:520upx;"
						></image>
					</view>
				</swiper-item>
			</swiper>
			<view style="padding:60upx 40upx 40upx;display: flex;justify-content: space-between;align-items: center;">
				<span style="font-size: 32upx;color:#fff;">游戏圈</span>
				<span style="display: flex; align-items: center;">
					<span style="color:#fff;opacity: 0.5;font-size: 24upx;margin-right:4upx;">更多</span>
					<image src="../../static/bg/right2.png" style="width:16upx;height:32upx;"></image>
				</span>
			</view>
			<view class="game">
				<view>
					<image src="../../static/bg/BetDice.png"></image>
					<span>BetDice</span>
				</view>
				<view>
					<image src="../../static/bg/angry.png"></image>
					<span>Angry</span>
				</view>
				<view>
					<image src="../../static/bg/nano.png"></image>
					<span>Nano</span>
				</view>
				<view style="margin-right:0;">
					<image src="../../static/bg/moto.png"></image>
					<span>MOTO</span>
				</view>
				<view>
					<image src="../../static/bg/war.png"></image>
					<span>The War</span>
				</view>
				<view>
					<image src="../../static/bg/row.png"></image>
					<span>Row</span>
				</view>
				<view>
					<image src="../../static/bg/non.png"></image>
					<span>Non</span>
				</view>
				<view style="margin-right:0;">
					<image src="../../static/bg/thor.png"></image>
					<span>Thor</span>
				</view>	
			</view>
			<share 
				ref="share" 
				:contentHeight="580"
				:shareList="shareList"
			></share>
		</view>
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
					
				},
				shareList: [],
				
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

<style lang="scss" scoped>
	.carousel{
		width:670upx;
		height:520upx;
		background:#fff;
		margin:0upx 40upx 0;
		.image-wrapper{
			
			width:100%;
			height:100%;
			image{
				width:100%;
				height:100%;
				
			}
		}
	}
	.game{
		display: flex;
		flex-wrap:wrap;
		width:100%;
		padding:0 40upx;
		justify-content:space-between;
		view{
			margin-right:24upx;
			display: flex;
			flex-direction: column;
			image{
				
				width:132upx;
				height:132upx;
			}
			span{
				color:#fff;
				font-size:24upx;
				text-align: center;
				margin:24upx 0 36upx;
			}
		}
	}
</style>
