<template>
	<scroll-view class="tab-box">
		<view class="tabs">
			<block v-for="(item,index) in tabs" :key="item.id">
				<view :class="['tab-item',activeTab == index?'active':'']" @click="toggleActive(index)">{{item.text}}</view>
			</block>
		</view>
	</scroll-view>
</template>

<script>
	export default {
		props:{
			tabs:{
				type:Array,
				default:[]
			}
		},
		data() {
			return {
				activeTab:0
			};
		},
		mounted(){
		},
		methods:{
			toggleActive(index){
				this.activeTab = index;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.tab-box{
		width:750upx;
		.tabs{
			display:flex;
			justify-content:center;
			flex-wrap:nowrap;
			align-items:center;
			.tab-item{
				padding:0upx 46upx;
				color:#c7c7c7;
				font-size:28upx;
				// transition:all .2s;
				&.active{
					font-size: 32upx;
					color:#fff;
					font-weight: bold;
				}
			}
		}
	}
</style>
