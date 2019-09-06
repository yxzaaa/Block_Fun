<template>
	<scroll-view class="tab-box" scroll-x="true" @scroll="scroll" scroll-left="0">
		<block v-for="(item,index) in tabs" :key="item.id">
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
			},
			scroll(e){
				console.log(e)
				this.old.scrollTop = e.detail.scrollTop
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
			line-height: 52upx;
			transition:all .2s;
			position:relative;
			&.active{
				transform: scale(1.1);
				color:#fff;
				font-weight: bold;
			}
		}
	}
</style>
