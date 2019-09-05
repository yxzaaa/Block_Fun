<template>
	<view>
		
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="收藏夹"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="guess">
			<view class="guess-list">
				<view 
					v-for="(item, index) in data.guessList" :key="index"
					class="guess-item"
					
				>
				
				
				<!-- 引入图片 -->
					<view style="line-height: 160upx;padding-right:40upx;">
						<image
							:src="item.src1" 
							@load="imageOnLoad('guessList', index)" 
							style="width:40upx;height:40upx;"
						></image>
					</view>
					<view class="image-wrapper">
					
							
						
						<image 
							:src="item.src" 
							:class="item.loaded" 
							mode="aspectFill"
							@load="imageOnLoad('guessList', index)" 
							style="width:160upx;height:160upx;"
						></image>
					</view>
					<!-- 图片描述 -->
					<view class="guess-content" style="margin-left:20upx;margin-top:0;">
						<span :class="{Skeleton:!loaded}" style="font-size: 28upx;color:#fff;">{{item.title}}</span>
						<text :class="{Skeleton:!loaded}" style="font-size:24upx;color:#999999;margin-top:12upx;">{{item.consume}} {{item.amount}}</text>
						<span :class="{Skeleton:!loaded}" style="margin-top:12upx;color:#DA53A2;">
							<span style="font-size:24upx;margin-right:8upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.symbol}}</span>
							<span style="display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[0]}}</span>
							<span style="font-size:24upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
							<span class="cut" style="position:absolute;right:50upx;display: inline-block;">
								<span style="margin-right:20upx;font-size:30upx;color:#fff;font-weight: bold;display: inline-block;"> - </span>
								<span style="display:inline-block;#99999;background:#280617;font-size:24upx;color:#fff;width:64upx;height:40upx;line-height: 40upx;text-align: center;">{{item.number}}</span>
								<span style="margin-left:20upx;font-size:30upx;color:#fff;font-weight: bold;display: inline-block;"> + </span>
							</span>
						</span>
					</view>
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
						type:'normal',
						text:'取消'
					},
					textbtn:{
						text:"完成",
						url:""
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

<style lang="scss" scoped>
	.guess {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items:center;
		padding:30upx 40upx 10upx;
		margin-top:150upx;
	}
	.guess-list {
		margin:0 auto;
		// display: flex;
		// flex-wrap: wrap;
		width:670upx;
		height:160upx;
	}
	.guess-item {
		display: flex;
		width:100%;
		padding-bottom: 40upx;
	
		.image-wrapper{
			width: 160upx;
			height: 160upx;
			border-radius: 10upx;
		}
		.guess-content{
			height:160upx;
			width:420upx;
			span,text{
				display: block;
			}
		}
	}
	
		
</style>
