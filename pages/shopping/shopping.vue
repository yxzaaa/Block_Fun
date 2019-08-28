<template>
	<view>
		<uni-background />
		<uni-nav-bar 
			title="购物" 
			layout="searchbtn" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container">
			<view class="banner-box">
<<<<<<< HEAD
				<image src="../../static/bg/dream.png" style="width:100%;height:726upx;"/>
=======
				<image src="../../static/bg/dream.png" style="width:100%;height:726upx"/>
>>>>>>> 7b3b303c93d51c23961c1958e575171daf4052a6
			</view>
			<view class="section-header">
				<text class="section-title">商品类别</text>
			</view>
			
			<view class="type-box">
				<block v-for="(item,index) in typeList" :key="index">
					<navigator style="margin-bottom:30upx;" :url="'../detail/detail?id='+item.id">
						<image :src="item.image" style="width:100%;display:block;height:240upx"/>
					</navigator>
				</block>
			</view>
			
			<view class="section-header">
				<text class="section-title">热门商品</text>
			</view>
			<view>
				<waterfall-flow :list="list" :loading="loading"></waterfall-flow>
			</view>
		</view>
	</view>
</template>

<script>
	
	import WaterfallFlow from '@/components/nairenk-waterfall-flow/nairenk-waterfall-flow.vue';// 瀑布流组件
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			WaterfallFlow,
		},
		data() {
			return {
				scroll:0,
				typeList:[
					{	
						id:1,
						image:"../../static/bg/daily.png"
					},
					{	
						id:2,
						image:"../../static/bg/numerical.png"
					},
					{	
						id:3,
						image:"../../static/bg/brand.png"
					},
					{	
						id:4,
						image:"../../static/bg/gift.png"
					}
				],
				list:[{
						id: 1,
						image: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1553493711400&di=e6c84132e52932ffaf8fc5025ed46824&imgtype=0&src=http%3A%2F%2Fimg5.duitang.com%2Fuploads%2Fitem%2F201303%2F31%2F20130331124639_svhNV.thumb.700_0.jpeg",
						title: "我的左手吗？呵…我把它送给了新世界",
						content:"消耗积分",
						consume:4000,
						symbol:"￥",
						money:"394.93"
						
					},{
						id: 2,
						image: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1553493784989&di=4e0dea29f039774a9478af73f5742920&imgtype=0&src=http%3A%2F%2Fphoto.16pic.com%2F00%2F51%2F49%2F16pic_5149719_b.jpg",
						title: "我是要成为海贼王的男人",
						content:"消耗积分",
						consume:4000,
						symbol:"￥",
						money:"3242"
					},{
						id: 3,
						image: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1553493871657&di=26eeaf4e2a8dc15be242029ce2073c8b&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201506%2F05%2F20150605173646_ehdVy.jpeg",
						title: "我不是天生的王者，但骨子里流着不让我低头的血液",
						content:"消耗积分",
						consume:4000,
						symbol:"￥",
						money:"1220"
					}],
				loading:false,
				navButtons:{
					// back:{
					// 	type:'circle'
					// },
					// share:{
					// 	type:'circle'
					// },
					// love:{
					// 	type:'circle'
					// },
					cart:{
						type:'normal',
						url:'../cart1/cart1'
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
