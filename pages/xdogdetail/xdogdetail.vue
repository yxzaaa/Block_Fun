<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="详情" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<div class="app-container full">
			<view class="user-info">
				<image :src="userInfo.avatar"></image>
				<text>{{userInfo.username}}</text>
			</view>
			<view class="user-count">
				<text>{{userInfo.usercount}}</text>
			</view>
			<view class="order-status">
				
			</view>
		</div>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground
		},
		data() {
			return {
				scroll:0,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					}
				},
				userInfo:{
					avatar:'../../static/avatar/fortoken.png',
					username:'Xdog',
					usercount:'+8089.23'
				}
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
	}
</script>

<style lang="scss" scoped>
	.user-info{
		width:750upx;
		display:flex;
		justify-content:center;
		align-items:center;
		padding:20upx 0;
		image{
			width:48upx;
			height:48upx;
			margin-right:20upx;
		}
		text{
			color:#fff;
			font-size: 32upx;
		}
	}
	.user-count{
		width:750upx;
		text-align:center;
		padding:30upx 0;
		text{
			color:#DA53A2;
			font-size: 52upx;
			font-family:'Montserrat-Bold';
		}
	}
</style>
