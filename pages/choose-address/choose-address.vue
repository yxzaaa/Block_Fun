<template>
	<view>
			
			<uni-background /> <!-- 背景色-->
			<!-- 导航栏 -->
			<uni-nav-bar 	
				title="选择收货地址"
				textColor="#fff"
				:opacity="scroll"
				:buttons="navButtons"
			/>
			<view class="app-container full">
				<navigator class="tosite" url="../address/addressManage">
					<view class="site">
						<span class="person-info">
							<span class="name-phone">
								<span class="name" style="font-size:28upx;color:#fff;">王依依</span>
								<span class="phone" style="font-size:24upx;color:#999999;;">133xxxx1232</span>
							</span>
							<span class="adress" style="font-size:24upx;display: block;color:#999999;;">北京市朝阳区朝阳路朝阳小区10号楼102</span>
						</span>
					</view>
					<span style="border-left:1px solid rgba(255,255,255,0.4);display: block;padding-left:40upx;font-size:24upx;color:#DA53A2;font-family: PingFang SC;width:80upx;">编辑</span>
				</navigator>
				<navigator class="tosite" url="../address/addressManage">
					<view class="site">
						<span class="person-info">
							<span class="name-phone">
								<span class="name" style="font-size:28upx;color:#fff;">王依依</span>
								<span class="phone" style="font-size:24upx;color:#999999;;">133xxxx1232</span>
							</span>
							<span class="adress" style="font-size:24upx;display: block;color:#999999;;">北京市朝阳区朝阳路朝阳小区10号楼102</span>
						</span>
					</view>
					<span style="border-left:1px solid rgba(255,255,255,0.4);display: block;padding-left:40upx;font-size:24upx;color:#DA53A2;font-family: PingFang SC;width:80upx;">编辑</span>
				</navigator>
				<view class="fixed-buttons">
					<view class="button-group">
						<fun-button value="创建新地址" width="670upx"  large url="../address/addressManage"></fun-button>
					</view>
				</view>
			</view>
	</view>
</template>

<script>
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import FunButton from '@/components/fun-button.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			FunButton
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
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		
	}

		
	
</script>

<style lang="scss" scoped>
	.tosite{
		width:750upx;
		height:160upx;
		padding:40upx;
		border-bottom:1px solid rgba(255,255,255,0.1);
		display:flex;
		align-items:center;
		justify-content:space-between;
		.site{
			width:686upx;
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
	.button-group{
		width:670upx;
	}
</style>
