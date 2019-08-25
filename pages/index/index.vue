<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="Blockfun" textColor="#fff" :opacity="scroll" layout="left" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container">
			<view class="banner">
				<img src="static/banner.jpg" alt="">
			</view>
			<ul cass="button-list">
				
			</ul>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	export default{
		components:{
			UniNavBar,
			UniBackground
		},
		data(){
			return {
				scroll:0,
				navButtons:{
					search:{
						type:'normal'
					}
				}
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
	}
</script>

<style lang="scss" scoped>
	p{
		color:#fff;
	}
	.banner{
		width:690upx;
		img{
			width:100%;
		}
	}
</style>
