<template>
	<view v-if="loading" class="Skeleton" :style="{width:width,height:height,display:display}">
		
	</view>
</template>

<script>
	export default {
		props:{
			width:{
				type:String,
				default:'100%'
			},
			height:{
				type:String,
				default:'100%'
			},
			display:{
				type:String,
				default:'block'
			},
			loading:{
				type:Boolean,
				default:true
			}
		},
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss">

</style>
