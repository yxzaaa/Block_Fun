<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			layout="search" 
			:opacity="scroll"
			:buttons="navButtons"
			@input="searchInput"
			@search="search"
		/>
		<view class="app-container full" style="padding-left:40upx;padding-right:40upx;">
			<view class="history-box" v-if="historyList.length>0 && !showItem">
				<view style="display: flex;justify-content: space-between;padding:30upx 0;">
					<text style="color:#fff;font-size: 26upx;">历史记录</text>
					<text style="color:rgba(255,255,255,0.5);font-size: 26upx;" @click="clearHis">清除历史</text>
				</view>
				<view class="history-list">
					<view class="history-item" v-for="(item,index) in historyList" @click="search(item)">{{item}}</view>
				</view>
			</view>
			<view v-if="itemList.length == 0 && showItem" style="width:670upx;">
				<image src="../../static/bg/orders/search_res.png" style="width:670upx;height:420upx;"></image>
			</view>
			<view class="item-box" v-if="showItem">
				<navigator
					v-for="(item, index) in itemList" :key="item.id"
					class="guess-item"
					:url="'../detail/detail?id='+item.id"
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
					textbtn:{
						text:'取消',
					} 
				},
				historyList:[],
				searchText:'',
				showItem:false,
				itemList:[]
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onShow(){
			if(uni.getStorageSync('search_history')){
				uni.getStorage({
					key:'search_history',
					success:res=>{
						this.historyList = res.data;
					}
				})
			}
		},
		methods:{
			searchInput(val){
				this.searchText = val;
				if(val === ''){
					this.showItem = false;
				}
			},
			clearHis(){
				uni.removeStorage({
					key:'search_history',
					success:res=>{
						this.historyList = [];
					}
				});
			},
			search(text){
				if(text && text.length>0){
					this.searchText = text;
					this.$http({
						url:'/mall/search?kw='+this.searchText,
						success:res=>{
							console.log(res);
							if(res.code == 200){
								//设置搜索结果
								this.itemList = res.data.item;
								this.showItem = true;
							}
						}
					})
				}else if(this.searchText.length>0){
					this.$http({
						url:'/mall/search?kw='+this.searchText,
						success:res=>{
							console.log(res);
							if(res.code == 200){
								if(uni.getStorageSync('search_history')){
									uni.getStorage({
										key:'search_history',
										success:val=>{
											if(this.searchText.length>0){
												val.data.push(this.searchText);
												this.historyList = val.data;
												uni.setStorage({
													key:'search_history',
													data:this.historyList
												})
											}
										}
									})
								}else{
									uni.setStorageSync('search_history',[this.searchText]);
								}
								//设置搜索结果
								this.itemList = res.data.item;
								this.showItem = true;
								console.log(this.itemList);
							}
						}
					})
				}
			},
		}
	}
</script>

<style lang="scss" scoped>
	.history-list{
		width:670upx;
		display:flex;
		justify-content:flex-start;
		flex-wrap:wrap;
		.history-item{
			padding:20upx;
			color:rgba(255,255,255,0.5);
			background:  rgba(21, 3, 11, 0.3);
			font-size: 26upx;
			margin-right:20upx;
			margin-bottom:20upx;
			border-radius: 8upx;
		}
	}
	.item-box {
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
</style>