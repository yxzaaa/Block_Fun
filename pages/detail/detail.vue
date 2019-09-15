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
							:src="item" 
							mode="aspectFill"
							style="width:100%;height:738upx;"
						></image>
					</view>
				</swiper-item>
			</swiper>
			<view class="info">
				<view class="title">
					<span style="margin-top:40upx;">
						<span style="font-size:30upx;margin-right:10upx;font-family:'Montserrat-Bold';">￥</span>
						<span style="font-size:40upx;font-family:'Montserrat-Bold';">{{price.split('.')[0]}}</span>
						<span style="font-size: 30upx;font-family:'Montserrat-Bold';">{{price.split('.')[1]?'.' + price.split('.')[1]:''}}</span>
					</span>
					
					<text style="color:#999999;font-size:24upx;margin-top:16upx;">消耗积分 {{credit}}</text>
					<text style="background:#DA53A2;height:32upx;width:64upx;text-align: center;font-size:24upx;color:#fff;margin-top:16upx;">{{catname}}</text>
					<text style="color:#fff;font-size: 32upx;margin-top:16upx;">{{title}}</text>
					<text style="color:#999999;font-size: 24upx;margin-top:16upx;width:670upx;line-height:44upx;">{{content}}</text>
				</view>
			</view>
			
			<!-- 相关推荐-->
			<view class="guess">
				<view class="section-tit">相关推荐</view>
				<view class="guess-list">
					<view 
						v-for="(item, index) in guessList" :key="item.itemid"
						class="guess-item"
						url="../detail/detail"
					>
					<!-- 引入图片 -->
						<view class="image-wrapper">
							<!-- <image 
								:src="item.src" 
								mode="aspectFill"
							></image> -->
						</view>
						<!-- 图片描述 -->
						<view class="guess-content" style="margin-left:20upx;margin-top:0;">
							<span class='title clamp' style="font-size:24upx;color:#fff;white-space: normal;width:448upx;">{{item.title}}</span>
							<span class="clamp" style="font-size:24upx;color:#999999;margin-top:14upx;">消耗积分 {{item.credit}}</span>
							<span class="clamp" style="margin-top:8upx;color:#DA53A2;font-family:'Montserrat-Bold';">
								<span style="font-size:24upx;margin-right:8upx;font-family:'Montserrat-Bold';">￥</span>
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
					<fun-button value="加入购物车" type="light" width="240upx" large @handle="addCart"></fun-button>
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
				},
				credit:'',
				catname:'',
				title:'',
				content:'',
				price:'',
				imgList:[],
				guessList:[]
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(option){
			this.$http({
				url:'/mall/show',
				data:{
					itemid:option.id,
				},
				success:res=>{
					if(res.code == 200){
						this.credit = res.result.credit;
						this.catname = res.result.catname;
						this.title = res.result.title;
						this.content = res.result.content;
						this.imgList = res.result.img;
						this.price = res.result.price;
						this.guessList = res.result.rec
					}
				}
			})
		},
		methods:{
			addCart(res){
				this.$http({
					url:'/mall/cart',
					data:{
						
					},
					success:res=>{
						console.log(res);
						
					}
					
				})
			   
			}
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
