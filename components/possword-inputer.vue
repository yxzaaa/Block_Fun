<template>
	<view class="password-box">
		<text class="item-text">{{password[0]}}</text>
		<text class="item-text">{{password[1]}}</text>
		<text class="item-text">{{password[2]}}</text>
		<text class="item-text">{{password[3]}}</text>
		<text class="item-text">{{password[4]}}</text>
		<text class="item-text">{{password[5]}}</text>
		<input type="number" class="password-input" maxlength="6" v-model="password" focus @blur="inputBlur"/>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				password:'',
				setFocus:true
			};
		},
		methods:{
			inputBlur(){
				this.password = '';
			},
		}
	}
</script>

<style lang="scss" scoped>
	.password-box{
		width:100%;
		display:flex;
		justify-content:space-between;
		align-items:center;
		position:relative;
		.password-input{
			position: absolute;
			top:0px;
			left:0px;
			width:100%;
			height:100%;
			opacity: 0;
		}
		.item-text{
			display: block;
			width:64upx;
			height:64upx;
			border-radius: 10upx;
			background: #F2F8FF;
			line-height: 64upx;
			text-align: center;
			font-size: 32upx;
			color:#DA53A2;
			font-family:'Montserrat-Bold';
		}
	}
</style>
