<template>
	<!-- 商品详情页1 -->
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			:opacity="scroll"
			:buttons="navButtons"	
			@handle="buttonHandler"
		/>
		<view class="addcart-item" v-if="adding"></view>
		<view class="app-container fixbutton">
			<uni-popup ref="popup" type="bottom">
				<view class="choose">
					<view class="goods">
						<view class="goods-info">
							<view class="img">
								<image :src="imgList[0]"></image>
							</view>
							<view class="title">
								<span>
									<span style="font-size:30upx;font-family:'Montserrat-Bold';">￥</span>
									<span style="font-size:40upx;font-family:'Montserrat-Bold';">{{price.split('.')[0]}}</span>
									<span style="font-size: 30upx;font-family:'Montserrat-Bold';">{{price.split('.')[1]?'.' + price.split('.')[1]:''}}</span>
								</span>
								<text style="color:#999999;font-size:24upx;margin-top:16upx;">库存 {{currStock}} 件</text>
								<text style="color:#999999;font-size:24upx;margin-top:16upx;">消耗积分 {{credit}}</text>
							</view>
						</view>
						<view class="img" @click = "$refs.popup.close()">
							<image src="../../static/bg/close.png"></image>
						</view>
					</view>
					<scroll-view style="width:100%;height:452upx;" scroll-y>
						<block v-for="(elem,index) in skuNames" :key="index">
							<view class="pramabox" >
								<span>{{elem.title}}</span>
								<view class="param">
									<span 
										v-for="(val,i) in elem.item" 
										:key="i" 
										v-if="i>0"
										@click="setSkuActive(index,i,val.stock)" 
										:class="[i==skuActive[index].active?'active':'',val.stock === 0?'nostock':'']"
									>{{val.value}}</span>
								</view>
							</view>
						</block>
						<view class="numberbox">
							<span>数量</span>
							<span class="cut">
								<image :src="imageLib.jian" style="width:40upx;height:40upx;" @click="buyCount = buyCount>1?buyCount-1:1"></image>
								<span>{{buyCount}}</span>
								<image :src="imageLib.add" style="width:40upx;height:40upx;" @click="addCount"></image>
							</span>
						</view>
					</scroll-view>
					<view class="fixed-buttons" style="display: flex;justify-content: center;align-items: center;">
						<view class="button-group" style="width:670upx;">
							<fun-button value="确定" width="670upx" large @handle = "modalConfirm"></fun-button>
						</view>
					</view>
				</view>
			</uni-popup>
			<swiper v-if="!loading" class="carousel" indicator-dots=true circular=true interval="3000" duration="700" indicator-active-color="#DA53A2">
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
			<Skeleton height="720upx" :loading="loading"></Skeleton>
			<view class="info" v-if="!loading">
				<view class="title">
					<span style="margin-top:40upx;">
						<span style="font-size:30upx;margin-right:4upx;font-family:'Montserrat-Bold';">￥</span>
						<span style="font-size:40upx;font-family:'Montserrat-Bold';">{{price.split('.')[0]}}</span>
						<span style="font-size: 30upx;font-family:'Montserrat-Bold';">{{price.split('.')[1]?'.' + price.split('.')[1]:''}}</span>
					</span>
					<text style="color:#999999;font-size:24upx;margin-top:16upx;">消耗积分 {{credit}}</text>
					<text style="background:#DA53A2;height:32upx;width:64upx;text-align: center;font-size:24upx;color:#fff;margin-top:16upx;">{{catname}}</text>
					<text style="color:#fff;font-size: 32upx;margin-top:16upx;">{{title}}</text>
					<text style="color:#999999;font-size: 24upx;margin-top:16upx;width:670upx;line-height:44upx;">{{content}}</text>
				</view>
			</view>
			<view v-if="loading" style="padding:40upx;">
				<Skeleton width="200upx" height="60upx" :loading="loading"></Skeleton>
				<Skeleton width="200upx" height="32upx" :loading="loading"></Skeleton>
				<Skeleton width="64upx" height="32upx" :loading="loading"></Skeleton>
				<Skeleton height="80upx" :loading="loading"></Skeleton>
				<Skeleton height="320upx" :loading="loading"></Skeleton>
			</view>
			
			<!-- 相关推荐-->
			<view class="guess">
				<view class="section-tit">相关推荐</view>
				<view class="guess-list">
					<navigator 
						v-for="(item, index) in guessList" :key="item.itemid"
						class="guess-item"
						:url="'../detail/detail?id='+item.itemid"
						 v-if="!loading"
					>
					<!-- 引入图片 -->
						<view class="image-wrapper">
							<image 
								:src="item.img" 
								mode="aspectFill"
							></image>
						</view>
						<!-- 图片描述 -->
						<view class="guess-content" style="margin-left:20upx;margin-top:0;">
							<view class='title clamp' style="height:106upx;font-size:28upx;color:#fff;white-space: normal;width:450upx;">{{item.title.length>36?item.title.substring(0,36)+' ...':item.title}}</view>
							<span class="clamp" style="font-size:24upx;color:#999999;margin-top:14upx;">消耗积分 {{item.credit}}</span>
							<span class="clamp" style="margin-top:8upx;color:#DA53A2;font-family:'Montserrat-Bold';">
								<span style="font-size:24upx;margin-right:8upx;font-family:'Montserrat-Bold';">￥</span>
								<span style="font-family:'Montserrat-Bold';">{{item.price.split('.')[0]}}</span>
								<span style="font-size:24upx;font-family:'Montserrat-Bold';">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
							</span>
						</view>
					</navigator>
					<Skeleton height="200upx" :loading="loading"></Skeleton>
				</view>
			</view>
			
			<!-- 底部按钮 -->
			<view class="fixed-buttons" style="display: flex;justify-content: space-between;align-items: center;">
				<view style="width:66upx;height:44upx;padding-left:30upx;" class="button-group">
					<image src="../../static/bg/listen.png" style="width:36upx;height:44upx;"></image>
				</view>
				
				<view class="button-group" style="width:500upx;">
					<fun-button value="加入购物车" type="light" width="240upx" large @handle="openModal('cart')"></fun-button>
					<fun-button value="立即购买" width="240upx" large @handle="openModal('buy')"></fun-button>
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
	import uniPopup from "@/components/uni-popup/uni-popup.vue";
	import Skeleton from '@/components/Skeleton.vue';
	export default {
		components: {
			share,
			UniNavBar,
			UniBackground,
			FunButton,
			uniPopup,
			Skeleton
		},
		data() {
			return {
				scroll:0,
				loading:true,
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
						text:'handle',
						active:false
					},
					cart:{
						type:'circle',
						url:"../cart1/cart1",
						active:false
					},
				},
				imageLib:{
					add:'../../static/icons/ic_add.png',
					jian:'../../static/icons/ic_jian.png'
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
				buyCount:1,
				modalType:'',
				productId:'',
				skuNames:[],
				skuCodes:[],
				currStock:0,
				skuActive:[],
				totalStock:0,
				adding:false
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
						this.loading = false;
						this.credit = res.data.credit;
						this.catname = res.data.catname;
						this.title = res.data.title;
						this.content = res.data.content;
						this.imgList = res.data.img;
						this.price = res.data.price;
						this.guessList = res.data.rec;
						this.productId = res.data.id;
						this.navButtons.love.active = res.data.favorite == 1?true:false;
						this.skuNames = res.data.sku.name;
						this.skuCodes = res.data.sku.code;
						this.skuNames.forEach(elem=>{
							this.skuActive.push({
								title:elem.title,
								active:null
							})
							elem.item.map((val,index)=>{
								elem.item[index] = {
									value:val,
									stock:null
								}
							})
						})
						Object.keys(this.skuCodes).forEach(key => {
						     this.totalStock += parseInt(this.skuCodes[key]);
						})
						this.currStock = this.totalStock;
					}
				}
			})
		},
		methods:{ 
			openModal(type){
				this.modalType = type;
				this.$refs.popup.open();
			},
			setSkuActive(index,i,stock){
				if(stock !== 0){
					if(this.skuActive[index].active == i){
						this.skuActive[index].active = null;
					}else{
						this.skuActive[index].active = i;
					}
					var allSku = true;
					this.skuActive.map(item=>{
						if(item.active == null){
							allSku = false;
							return;
						}
					})
					if(allSku){
						var code = this.productId;
						this.skuActive.map(item=>{
							code += '-'+item.active;
						});
						this.currStock = this.skuCodes[code];
						this.buyCount = this.buyCount>this.currStock?this.currStock:this.buyCount;
					}
					if(this.skuNames.length == 2 && allSku){
						if(index == 0){
							this.skuNames[1].item.map((item,index1)=>{
								if(index1>0){
									var code = this.productId+'-'+i+'-'+index1;
									item.stock = this.skuCodes[code];
								}
							})
						}else if(index == 1){
							this.skuNames[0].item.map((item,index1)=>{
								if(index1>0){
									var code = this.productId+'-'+i+'-'+index1;
									item.stock = this.skuCodes[code];
								}
							})
						}
					}else if(this.skuNames.length == 2){
						this.currStock = 0;
						if(!this.skuActive[1].active && !this.skuActive[0].active){
							this.currStock = this.totalStock;
							this.skuNames[1].item.map((item,index1)=>{
								if(index1>0){
									var code = this.productId+'-'+i+'-'+index1;
									item.stock = null;
								}
							})
							this.skuNames[0].item.map((item,index1)=>{
								if(index1>0){
									var code = this.productId+'-'+i+'-'+index1;
									item.stock = null;
								}
							})
						}else if(index == 0 && this.skuActive[index].active){
							console.log(index);
							this.skuNames[1].item.map((item,index1)=>{
								if(index1>0){
									var code = this.productId+'-'+i+'-'+index1;
									item.stock = this.skuCodes[code];
									this.currStock += item.stock;
								}
							})
						}else if(index == 1 && this.skuActive[index].active){
							this.skuNames[0].item.map((item,index1)=>{
								if(index1>0){
									var code = this.productId+'-'+i+'-'+index1;
									item.stock = this.skuCodes[code];
									this.currStock += item.stock;
								}
							})
						}else if(index == 0 && !this.skuActive[index].active){
							this.skuNames[1].item.map((item,index1)=>{
								if(index1>0){
									var code = this.productId+'-'+i+'-'+index1;
									item.stock = null;
									this.currStock += this.skuCodes[code];
								}
							})
						}else if(index == 1 && !this.skuActive[index].active){
							this.skuNames[0].item.map((item,index1)=>{
								if(index1>0){
									var code = this.productId+'-'+i+'-'+index1;
									item.stock = null;
									this.currStock += this.skuCodes[code];
								}
							})
						}
					}
				}
			},
			addCount(){
				this.buyCount = this.buyCount<this.currStock?this.buyCount+1:this.currStock;
				if(this.buyCount == this.currStock){
					uni.showToast({
						title:'亲，达到库存上限了哟~',
						icon:'none'
					})
				}
			},
			modalConfirm(){
				var allSku = true;
				this.skuActive.map(item=>{
					if(item.active == null){
						allSku = false;
						return;
					}
				})
				if(allSku && this.buyCount>0){
					var code = this.productId;
					this.skuActive.map(item=>{
						code += '-'+item.active;
					})
					var skuInfo = {};
					skuInfo[code] = this.buyCount;
					if(this.modalType =='cart'){
						//添加购物车
						this.$http({
							url:'/mall/cart',
							type:'application/x-www-form-urlencoded',
							data:{
								action:'add',
								code,
								num:this.buyCount
							},
							success:res=>{
								console.log(res);
								if(res.code == 200){
									this.$refs.popup.close();
									uni.showToast({
										title:'商品已添加到购物车~',
										icon:'none'
									})
									this.adding = true;
									setTimeout(()=>{
										this.adding = false;
										this.navButtons.cart.active = true;
									},800)
								}else{
									this.$refs.popup.close();
									uni.showToast({
										title:res.message,
										icon:'none'
									})
								}
							}
						})
					}else if(this.modalType == 'buy'){
						//设置商品代码
						uni.setStorage({
							key:'skuCode',
							data:[skuInfo],
							success:()=>{
								//立即购买
								uni.navigateTo({
									url: '../order-management/order-management',
								});
							}
						})
					}
				}else{
					uni.showToast({
						title:'亲，请选择商品规格哦~',
						icon:'none'
					})
				}
			},
			buttonHandler(type){
				if(type == 'love'){
					if(this.navButtons.love.active == false){
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
										title:'商品收藏成功~',
										icon:'none'
									})
									this.navButtons.love.active = true;
								}
							}
						})
					}else{
						uni.navigateTo({
							url: '../favorite/favorite',
						});
					}
				}else if(type == 'cart'){
					
				}
			}
		},
	}
</script>

<style lang="scss" scoped>
	.addcart-item{
		position:fixed;
		z-index:1000;
		bottom:calc(100vh - 100upx);
		left:660upx;
		width:12upx;
		height:12upx;
		border-radius: 6upx;
		background: #DA53A2;
		animation: addcart 0.6s ease-in-out 1;
		opacity: 0;
	}
	@keyframes addcart{
		0%{
			bottom:20upx;
			left:40upx;
			width:670upx;
			height:80upx;
			border-radius: 40upx;
			opacity: 0;
		}
		30%{
			bottom:300upx;
			left:380upx;
			width:80upx;
			height:80upx;
			border-radius: 40upx;
			opacity: 0.8;
		}
		100%{
			bottom:calc(100vh - 100upx);
			left:660upx;
			width:12upx;
			height:12upx;
			border-radius: 12upx;
			opacity: 0.6;
		}
	}
	.choose{
		width:750upx;
		height:800upx;
		background: #281920;
		padding:40upx;
		.goods{
			display: flex;
			align-items: flex-start;
			justify-content: space-between;
			padding-bottom:30upx;
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
			padding-top: 40upx;
			span{
				font-size: 28upx;
				color:#ffffff;
			}
			.param{
				display: flex;
				justify-content: flex-start;
				padding-top:40upx;
				span{
					color:#ffffff;
					padding:24upx;
					background:#15030B;
					border-radius: 8upx;
					margin-right:20upx;
					font-size: 24upx;
					&.active{
						box-shadow: 0px 0px 1upx 2upx #DA53A2 inset;
						color:#DA53A2;
					}
					&.nostock{
						opacity: 0.5;
					}
				}
			}
		}
		.numberbox{
			display: flex;
			justify-content: space-between;
			align-items: flex-start;
			padding:60upx 0upx;
			span{
				color:#ffffff;
				font-size:28upx;
				line-height:64upx;
			}
			span.cut{
				display: flex;
				justify-content: space-between;
				width:200upx;
				align-items: center;
				span{
					line-height: 64upx;
					font-size: 26upx;
					text-align: center;
					padding:0upx 30upx;
					background: #15030B;
					border-radius: 8upx;
					
				}
			}
		}
	}

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
			overflow:hidden;
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
