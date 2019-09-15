<template>
	<!-- 商品详情页1 -->
	<view>
		<uni-background />
		<uni-nav-bar 
			:opacity="scroll"
			:buttons="navButtons"	
			@handle="buttonHandler"
		/>
		<view class="app-container fixbutton">
			<view class="choose-box" v-if="specModal">
				<view class="choose">
					<view class="goods">
						<view class="goods-info">
							<view class="img">
								<image src="../../static/bg/detail1.png"></image>
							</view>
							<view class="title">
								<span>
									<span style="font-size:30upx;font-family:'Montserrat-Bold';">￥</span>
									<span style="font-size:40upx;font-family:'Montserrat-Bold';">354</span>
									<span style="font-size: 30upx;font-family:'Montserrat-Bold';">.12</span>
								</span>
								<text style="color:#999999;font-size:24upx;margin-top:16upx;">消耗积分 4000</text>
							</view>
						</view>
						<view class="img" @click = "specModal=false">
							<image src="../../static/bg/close.png"></image>
						</view>
					</view>
					<view class="pramabox">
						<span>参数</span>
						<view class="param">
							<span>10ml</span>
							<span>50ml</span>
							<span>100ml</span>
							<span>200ml</span>
						</view>
					</view>
					<view class="numberbox">
						<span>数量</span>
						<span class="cut" style="position: relative;top:-4upx;">
							<span style="margin-right:20upx;font-size:36upx;color:#fff;font-weight: bold;display: inline-block;"> - </span>
							<span style="display:inline-block;#99999;background: #15030B;font-size:28upx;color:#fff;width:72upx;line-height: 40upx;text-align: center;"> 0 </span>
							<span style="margin-left:20upx;font-size:36upx;color:#fff;font-weight: bold;display: inline-block;"> + </span>
						</span>
					</view>
					<view class="fixed-buttons" style="display: flex;justify-content: center;align-items: center;">
						<view class="button-group" style="width:670upx;">
							<fun-button value="确定" width="670upx" large @handle = "modalConfirm"></fun-button>
						</view>
					</view>
				</view>
			</view>
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
					<fun-button value="加入购物车" type="light" width="240upx" large @handle="openModal('cart')"></fun-button>
					<fun-button value="立即购买" width="240upx" large url="../order-management/order-management" @handle="openModal('buy')"></fun-button>
				</view>
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
						type:'circle',
						classify:'share',
						text:'handle'
					},
					love:{
						type:'circle',
						classify:'love',
						text:'handle'
						
					},
					cart:{
						type:'circle',
						url:"../cart1/cart1",
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
				guessList:[],
				codeList:[],
				specModal:false,
				modalType:'',
				productId:''
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(option){
			this.$http({
				url:'/mall/show?itemid='+option.id,
				success:res=>{
					console.log(res);
					if(res.code == 200){
						this.credit = res.data.credit;
						this.catname = res.data.catname;
						this.title = res.data.title;
						this.content = res.data.content;
						this.imgList = res.data.img;
						this.price = res.data.price;
						this.guessList = res.data.rec;
						this.productId = res.data.id;
					}
				}
			})
		},
		methods:{
			openModal(type){
				this.specModal = true;
				this.modalType = type;
			},
			modalConfirm(){
				if(this.modalType =='cart'){
					this.specModal = false;
					this.$http({
						url:'/mall/cart',
						type:'application/x-www-form-urlencoded',
						data:{
							code:'',
						},
						success:res=>{
							console.log(res);
							
						}
						
					})
				}else{
					
				}
			},
			buttonHandler(type){
				if(type == 'love'){
					this.$http({
						url:'/member/favorite',
						type:'application/x-www-form-urlencoded',
						data:{
							action:'add',
							id:this.productId,
						},
						success:res=>{
							if(res.code == 200){
								uni.showToast({
									title:'商品收藏成功~'
								})
							}
						}
					})
				}
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
	.choose-box{
		width:750upx;
		height:100vh;
		background:rgba(0,0,0,0.5);
		position: fixed;
		left:0;
		top:0;
		z-index:1000;
		.choose{
			width:750upx;
			height:716upx;
			background: #281920;
			position: absolute;
			bottom:0;
			padding:40upx;
			.goods{
				display: flex;
				align-items: flex-start;
				justify-content: space-between;
				.goods-info{
					display:flex;
				
					.img{
						border-radius:8upx;
						width:160upx;
						height:160upx;
						overflow:hidden;
						image{
							width:100%;
							height:100%;
						}
					}
					.title{
						display: flex;
						flex-direction: column;
						justify-content: flex-end;
						margin-left:20upx;
						span{
							color: #DA53A2;
							font-weight: 600;
						}
						text{
							color:#999999;
							margin-top:20upx;
						}
					}
				}
				
				.img{
					width:40upx;
					height:40upx;
					image{
						width:100%;
						height:100%;
					}
				}
			}
			.pramabox{
				margin-top: 60upx;
				span{
					font-size: 28upx;
					color:#ffffff;
				}
				.param{
					display: flex;
					justify-content: flex-start;
					margin-top:40upx;
					span{
						color:#ffffff;
						padding:28upx 20upx;
						background:#15030B;
						border-radius: 8upx;
						margin-right:20upx;
						font-size: 24upx;
						
					}
				}
			}
			.numberbox{
				display: flex;
				justify-content: space-between;
				align-items: flex-start;
				margin-top:60upx;
				span{
					color:#ffffff;
					font-size:28upx;
				}
			}
		}
	}
	
</style>
