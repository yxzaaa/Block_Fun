<template>
	<view 
		:class="['fun-btn',type?type:'',large?'large':'']" 
		:style="{width:width,color:color,background:background}" 
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
			},
			background:{
				type:String,
				default:''
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
				if(this.url != ''){
					uni.navigateTo({
						url:this.url
					})
				}else{
					this.$emit('handle','');
				}
			}
		}
	}
</script>

<style lang="scss">
	.fun-btn{
		height:64upx;
		line-height: 64upx;
		font-size: 26upx;
		border-radius: 32upx;
		background:#DA53A2;
		color:#fff;
		padding:0px 36upx;
		display:flex;
		justify-content: center;
		align-items: center;
		position:relative;
		transition:all .1s;
		text{
			vertical-align:middle;
			display: inline-block;
		}
		&:active{
			opacity: 0.8;
		}
		.button-icon{
			width:24upx;
			height:24upx;
			margin:20upx 0upx;
			margin-right:14upx;
			display: inline-block;
			vertical-align:middle;
		}
		&.light{
			background: #fff;
			color:#DA53A2;
		}
		&.text{
			background: transparent;
			color:#c7c7c7;
			padding:0px;
		}
		&.large{
			font-size: 30upx;
			line-height: 80upx;
			height:80upx;
			border-radius: 40upx;
		}
		&.large .button-icon{
			width:30upx;
			height:30upx;
		}
	}
</style>
