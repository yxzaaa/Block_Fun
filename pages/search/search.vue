<template>
	<view>
		<uni-background />
		<uni-nav-bar 
			layout="search" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container">
			
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
				}
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
	}
</script>

<style lang="scss" scoped>

</style>