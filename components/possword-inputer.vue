<template>
	<view class="password-box">
		<text class="item-text" :style="{width:size,height:size,background:background}">{{password[0]}}</text>
		<text class="item-text" :style="{width:size,height:size,background:background}">{{password[1]}}</text>
		<text class="item-text" :style="{width:size,height:size,background:background}">{{password[2]}}</text>
		<text class="item-text" :style="{width:size,height:size,background:background}">{{password[3]}}</text>
		<text class="item-text" :style="{width:size,height:size,background:background}">{{password[4]}}</text>
		<text class="item-text" :style="{width:size,height:size,background:background}">{{password[5]}}</text>
		<input type="number" class="password-input" maxlength="6" v-model="password" @blur="inputBlur" :focus="true"/>
	</view>
</template>

<script>
	export default {
		props:{
			size:{
				type:String,
				default:'64upx'
			},
			background:{
				type:String,
				default:'#F2F8FF'
			}
		},
		data() {
			return {
				password:'',
				setFocus:true
			};
		},
		mounted(){
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
