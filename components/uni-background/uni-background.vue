<template>
	<div class="fixed-container">
		
	</div>
</template>

<script>
	export default{
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
		background-image:url(../../static/bg.jpg);
		background-size:100% auto;
		background-repeat: no-repeat;
		background-color:#15030B;
		z-index:-1;
	}
</style>
