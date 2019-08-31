<template>
	<div class="fixed-container" :style="{backgroundImage:'url('+src+')'}">
		
	</div>
</template>

<script>
	export default{
		props:{
			src:{
				type:String,
				default:"../../static/bg.jpg"
			}
		},
		data(){
			return {
				
			}
		}
	}
</script>

<style lang="scss" scoped>
	.fixed-container{
		position: fixed;
		width:750upx;
		height:100vh;
		top:0;
		left:0;
		background-size:100% auto;
		background-repeat: no-repeat;
		background-color:#15030B;
		z-index:-1;
	}
</style>
