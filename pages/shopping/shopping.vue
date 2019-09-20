<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			title="购物" 
			layout="searchbtn" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container">
			<view class="banner-box" v-if="!loading">
				<swiper :indicator-dots="true" :autoplay="true" style="height:720upx;">
					<block v-for="(item,index) in bannerList"
					:key="index"
					>
						<swiper-item>
							<image :src="item" style="width:100%;height:100%"></image>
						</swiper-item>
					</block>
				</swiper>
			</view>
			<Skeleton height="720upx" :loading="loading"></Skeleton>
			<view class="section-header">
				<text class="section-title" style="color:#fff;font-size: 32upx;">商品类别</text>
			</view>
			
			<view class="type-box" v-if="!loading">
				<block v-for="(item,index) in typeList" :key="item.catid">
					<view style="margin-bottom:30upx;position: relative;height:240upx;">
						<image :src="item.img" style="width:100%;display:block;height:240upx"/>
						<span style="position: absolute; left:50upx;top:50%;margin-top:-32upx;line-height:64upx;font-size: 32upx;color:#fff;font-weight:bold;">{{item.title}}</span>
					</view>
				</block>
			</view>
			<view style="padding:40upx" v-if="loading">
				<Skeleton height="240upx" :loading="loading"></Skeleton>
				<Skeleton height="240upx" :loading="loading"></Skeleton>
				<Skeleton height="240upx" :loading="loading"></Skeleton>
				<Skeleton height="240upx" :loading="loading"></Skeleton>
			</view>
			
			<view class="section-header">
				<text class="section-title">热门商品</text>
			</view>
			<view v-if="!loading">
				<waterfall-flow :list="hotList" :loading="loading" @click="toDetail"></waterfall-flow>
			</view>
			<view style="padding:40upx" v-if="loading">
				<Skeleton height="240upx" :loading="loading"></Skeleton>
			</view>
		</view>
	</view>
</template>

<script>
	
	import WaterfallFlow from '@/components/nairenk-waterfall-flow/nairenk-waterfall-flow.vue';// 瀑布流组件
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import Skeleton from '@/components/Skeleton.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			WaterfallFlow,
			Skeleton
		},
		data() {
			return {
				scroll:0,
				bannerList:[],
				typeList:[],
				hotList:[],
				loading:true,
				navButtons:{
					cart:{
						type:'normal',
						url:'../cart1/cart1'
					},
				}
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
			this.$http({
				url:'/index/index',
				success:res=>{
					console.log(res);
					if(res.code == 200){
						this.bannerList = res.data.ad;
						this.typeList = res.data.cat;
						this.hotList = res.data.hot;
						this.loading = false;
					}
				}
			})
		},
		methods:{
			toDetail(res){
				uni.navigateTo({
					url:"../detail/detail?id="+res
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.banner-box{
		width:100%;
		img{
			width:100%;
		}
	}
	p{
		color:#fff;
	}
	.classify{
		margin-top:20px;
		margin-left:20px;
		font-size: 16px;
		color:#fff;
	}
	.type-box :first-child{
		margin-top:0 !important;
	}

</style>
