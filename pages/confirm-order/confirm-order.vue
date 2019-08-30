<template>
	<view>
		<uni-background />
		<uni-nav-bar 
			title="确认订单" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<navigator class="tosite" url="../choose-address/choose-address">
			<view class="site">
				<image src="../../static/bg/location.png" style="width:64upx;height:64upx;"></image>
				<span class="person-info">
					<span class="name-phone">
						<span class="name" style="font-size:28upx;color:#fff;">王依依</span>
						<span class="phone" style="font-size:24upx;color:#999999;;">133xxxx1232</span>
					</span>
					<span class="adress" style="font-size:24upx;display: block;color:#999999;;">北京市朝阳区朝阳路朝阳小区10号楼102</span>
				</span>
			</view>
			<image src="../../static/bg/right.png" style="width:40upx;height:40upx;"></image>
		</navigator>
		<!-- 购物车详情 -->
		<view class="guess">
			<view class="guess-list">
				<view 
					v-for="(item, index) in data.guessList" :key="index"
					class="guess-item"	
				>
		
				<!-- 引入图片 -->
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
						<span :class="{Skeleton:!loaded}" style="color:#DA53A2;position:relative;">
							<span style="font-size:24upx;margin-right:8upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.symbol}}</span>
							<span style="display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[0]}}</span>
							<span style="font-size:24upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
							<span class="cut" style="position:absolute;right:50upx;bottom:4upx;display: inline-block;">
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
					
				},
				data:{
					guessList:[{},{},{}],
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
		.tosite{
			width:750upx;
			height:64upx;
			padding:40upx;
			padding-top:214upx;
			padding-bottom:80upx;
			border-bottom:1px solid rgba(255,255,255,0.1);
			display:flex;
			align-items:center;
			justify-content:space-between;
			.tosite{
				display: flex;
			}
			.site{
				width:686upx;
				height:106upx;
				display: flex;
				align-items: center;
				.person-info{
					margin-left:20upx;
					.phone{
						margin-left:20upx;
					}
				}
				.toaddress{
					color:#fff;
					font-size:28upx;
					margin-left:32upx;
				}
			}
			
		}
		.guess {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items:center;
			padding:30upx 40upx 10upx;
		}
		.guess-list {
			margin:0 auto;
			// display: flex;
			// flex-wrap: wrap;
			width:670upx;
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
				span,text{
					display: block;
				}
			}
		}
	
	

</style>
