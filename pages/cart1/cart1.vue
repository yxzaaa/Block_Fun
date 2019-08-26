<template>
	<view>
		
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="购物车"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		
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
						style="width:200upx;height:200upx;"
					></image>
				</view>
				<!-- 图片描述 -->
				<view class="guess-content" style="margin-left:20upx;margin-top:0;">
					<text class='title clamp' :class="{Skeleton:!loaded}" style="font-size: 30upx;color:#fff;">{{item.title}}</text>
					<text class="clamp" :class="{Skeleton:!loaded}" style="font-size: 30upx;color:#fff;margin-top:10upx;">{{item.title2}}</text>
					<text class="clamp" :class="{Skeleton:!loaded}" style="font-size:30upx;color:#999999;margin-top:14upx;">{{item.consume}} {{item.amount}}</text>
					<text class="clamp" :class="{Skeleton:!loaded}" style="margin-top:14upx;color:#DA53A2;font-weight: bold;">
						<span style="font-size:24upx;margin-right:8upx;">{{item.symbol}}</span>
						<span>{{item.price.split('.')[0]}}</span>
						<span style="font-size:24upx;">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
					</text>
				</view>
			</view>
		</view>
		
	</view>
		

</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import share from '@/components/share';
	export default {
		components:{
			UniNavBar,
			UniBackground,
		},
		data() {
			return {
				scroll:0,
				navButtons:{
					back:{
						type:'normal'
					},
					textbtn:{
						text:"管理"
					},
					
				},
				loaded:false,
				data:{
					guessList:[{},{}],
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
		}
		
	}
</script>

<style lang="scss">
	// 
	.guess-list {
		// display: flex;
		// flex-wrap: wrap;
		margin-top:200upx;
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
	}
	// 
	// 	.guess-content {
	// 		color:#999999;
	// 		// font-size: $font-sm;
	// 		// color: $font-color-light;
	// 		// &.Skeleton{
	// 		// 	width: 180upx;
	// 		// 	&.title{
	// 		// 		width: 140upx;
	// 		// 	}
	// 		// }
	// 		// &.title{
	// 		// 	font-size: $font-base+2upx;
	// 		// 	color: $font-color-dark;
	// 		// 	margin-top:16upx;
	// 		// 	margin-bottom: 8upx;
	// 		// }
	// 	}
	// 
</style>
