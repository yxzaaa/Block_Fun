<template>
	<view class="password-box">
		<text class="item-text" :style="{width:size,height:size,lineHeight:size,fontSize:fontSize,background:background}">{{password[0]}}</text>
		<text class="item-text" :style="{width:size,height:size,lineHeight:size,fontSize:fontSize,background:background}">{{password[1]}}</text>
		<text class="item-text" :style="{width:size,height:size,lineHeight:size,fontSize:fontSize,background:background}">{{password[2]}}</text>
		<text class="item-text" :style="{width:size,height:size,lineHeight:size,fontSize:fontSize,background:background}">{{password[3]}}</text>
		<text class="item-text" :style="{width:size,height:size,lineHeight:size,fontSize:fontSize,background:background}">{{password[4]}}</text>
		<text class="item-text" :style="{width:size,height:size,lineHeight:size,fontSize:fontSize,background:background}">{{password[5]}}</text>
		<text class="item-text" :style="{width:size,height:size,lineHeight:size,fontSize:fontSize,background:background}">{{password[6]}}</text>
		<text class="item-text" :style="{width:size,height:size,lineHeight:size,fontSize:fontSize,background:background}">{{password[7]}}</text>
		<input type="number" class="password-input" maxlength="8" v-model="password" @input="changeValue" :focus="true"/>
	</view>
</template>

<script>
	export default {
		props:{
			size:{
				type:String,
				default:'54upx'
			},
			fontSize:{
				type:String,
				default:'32upx'
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
			changeValue(e){
				this.$emit('input',e.detail.value);
			}
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
			width:54upx;
			height:54upx;
			border-radius: 8upx;
			background: #F2F8FF;
			line-height: 54upx;
			text-align: center;
			font-size: 32upx;
			color:#DA53A2;
			font-family:'Montserrat-Bold';
		}
	}
</style>
