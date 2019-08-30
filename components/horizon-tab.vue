<template>
	<scroll-view class="tab-box">
		<view class="tabs">
			<block v-for="(item,index) in tabs" :key="item.id">
				<view :class="['tab-item',activeTab == index?'active':'']" @click="toggleActive(index)" :style="{paddingLeft:padding+'upx',paddingRight:padding+'upx'}">{{item.text}}</view>
			</block>
		</view>
	</scroll-view>
</template>

<script>
	export default {
		props:{
			tabs:{
				type:Array
			},
			padding:{
				type:String
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
			width:auto;
			display:flex;
			justify-content:center;
			flex-wrap:nowrap;
			align-items:center;
			.tab-item{
				padding:0upx 20upx;
				color:rgba(255,255,255,.5);
				font-size:28upx;
				transition:all .2s;
				position:relative;
				&.active{
					transform: scale(1.1);
					color:#fff;
					font-weight: bold;
				}
			}
		}
	}
</style>
