<template>
	<view 
		:class="['fun-btn',type?type:'',large?'large':'']" 
		:style="{width:width,color:color}" 
		@click="buttonLink"
	>
		<image class="button-icon" :src="icon" v-if="icon" />
		<text>{{value}}</text>
	</view>
</template>

<script>
	export default {
		props:{
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
			},
			color:{
				type:String,
				default:''
			},
			url:{
				type:String,
				default:''
			},
			large:{
				type:Boolean,
				default:false
			}
		},
		data() {
			return {
				
			};
		},
		mounted(){
		},
		methods:{
			buttonLink(){
				uni.navigateTo({
					url:this.url
				})
			}
		}
	}
</script>

<style lang="scss">
	.fun-btn{
		height:64upx;
		line-height: 60upx;
		font-size: 26upx;
		border-radius: 32upx;
		background:#DA53A2;
		color:#fff;
		padding:0px 36upx;
		display:inline-block;
		text-align:center;
		
		text{
			vertical-align:middle;
			display: inline-block;
		}
		.button-icon{
			width:24upx;
			height:24upx;
			margin:20upx 0upx;
			margin-right:14upx;
			display: inline-block;
			vertical-align:middle;
		}
		&.large .button-icon{
			width:26upx;
			height:26upx;
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
		&.large{
			font-size: 28upx;
			color:#DA53A2;
		}
	}
</style>
