<template>
	<scroll-view class="tab-box" scroll-x="true" scroll-left="0">
		<block v-for="(item,index) in tabs" :key="index">
			<view :class="['tab-item',activeTab == index?'active':'']" @click="toggleActive(index)" :style="{paddingLeft:padding+'upx',paddingRight:padding+'upx'}">{{item.text}}</view>
		</block>
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
				this.$emit('click',index);
			},
		}
	}
</script>

<style lang="scss" scoped>
	.tab-box{
		width:750upx;
		text-align:center;
		white-space: nowrap;
		.tab-item{
			display: inline-block;
			padding:0upx 20upx;
			color:rgba(255,255,255,.5);
			font-size:28upx;
			line-height: 72upx;
			transition:all .1s;
			position:relative;
			&.active{
				transform: scale(1.1);
				color:#fff;
			}
		}
	}
</style>
