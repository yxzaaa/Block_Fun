<template>
	<view :class="['fun-btn',type?type:'',block?'block':'']" :style="{width:width+'upx'}">
		<image class="button-icon" :src="icon" v-show="icon"/>
		<text>{{value}}</text>
	</view>
</template>

<script>
	export default {
		props:{
			block:{
				type:Boolean,
				default:false
			},
			icon:{
				type:String,
				default:''
			},
			type:{
				type:String,
				default:''
			},
			value:{
				type:String,
				default:''
			},
			width:{
				type:String,
				default:''
			}
		},
		data() {
			return {
				
			};
		},
		mounted(){
		}
	}
</script>

<style lang="scss">
	.fun-btn{
		height:64upx;
		line-height: 58upx;
		font-size: 26upx;
		border-radius: 32upx;
		background:#DA53A2;
		color:#fff;
		padding:0px 36upx;
		display:inline-block;
		text-align:center;
		.button-icon{
			width:24upx;
			height:24upx;
			margin:20upx 0upx;
			margin-right:20upx;
			display: inline-block;
			vertical-align:middle;
		}
		text{
			vertical-align:middle;
			display: inline-block;
		}
		&.block{
			display: block;
			width:100%;
		}
		&.light{
			background: #fff;
			color:#DA53A2;
		}
		&.text{
			background: transparent;
			color:#c7c7c7;
			padding:0px;
			font-size: 24upx;
		}
	}
</style>
