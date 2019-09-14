<template>
	<view>
		<uni-background />
		<uni-nav-bar
			title="新建收货地址"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="content" style="padding:40upx;">
			<view class="row b-b">
				<text class="tit" style="padding-top:0px;">收货人姓名</text>
				<input class="input" type="text" v-model="getterName" placeholder="请输入收货人姓名"/>
			</view>
			<view class="row b-b">
				<text class="tit">手机号</text>
				<input v-model="phone" class="input" type="number" placeholder="请输入11位手机号"/>
			</view>
			<view class="row b-b">
				<text class="tit">所属区域</text>
				<input v-model="area" class="input" type="text" placeholder="请选择市区">
					<picker mode="multiSelector">
						
					</picker>
				</input>
			</view>
			<view class="row b-b"> 
				<text class="tit">详细地址</text>
				<input v-model="address" class="input" type="text" placeholder="请选择市区"/>
			</view>
			
		</view>
		<view class="default" style="padding:30upx 40upx;display: flex;align-items: center;">
			<image src="../../static/bg/Group.png" style="width:40upx;height:40upx;margin-right:14upx;"></image>
			<text style="color:#fff;font-size: 24upx;">设为默认</text>
		</view>
		<view class="fixed-buttons">
			<view class="button-group">
				<fun-button @handle="addressPlus" value="保存并使用" width="670upx"  large url="../order-management/order-management"></fun-button>
			</view>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import FunButton from '@/components/fun-button.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			FunButton
		},
		data() {
			return {
				scroll:0,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					}
				},
				getterName:'',
				phone:'',
				area:'',
				address:'',
				isdefault:false
			}
		},
		onPageScroll(val){
			this.scroll=val.scrollTop
		},
		onLoad(option){
			
		},
		methods: {
			//收货地址数据
			
			//添加收货地址
			addressPlus(){
				this.$http({
					url:'/member/address',
					data:{
						action:'add',
						
					},
					success:res=>{
						
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.content{
		margin: 200upx 40upx 0;
		border-radius:10upx;
		background: #493740;
	}

	.row{
		display: flex;
		flex-direction: column;
		align-content: space-around;
		width:590upx;
		
		
		.tit{
			font-size: 30upx;
			color: #fff;
			padding-top:40upx;
			padding-bottom:10upx;
			display: block;
		}
		.input{
			flex: 1;
			font-size: 26upx;
			height:80upx;
			color: #fff;
			border-bottom:1px solid rgba(255,255,255,.1);
		}
		.icon-shouhuodizhi{
			font-size: 36upx;
			color: $font-color-light;
		}
	}
	.default-row{
		margin-top: 16upx;
		.tit{
			flex: 1;
		}
		switch{
			transform: translateX(16upx) scale(.9);
		}
	}
	.add-btn{
		display: flex;
		align-items: center;
		justify-content: center;
		width: 690upx;
		height: 80upx;
		margin: 60upx auto;
		font-size: $font-lg;
		color: #fff;
		background-color: $base-color;
		border-radius: 10upx;
		box-shadow: 1px 2px 5px rgba(219, 63, 96, 0.4);
	}
	.button-group{
		width:670upx;
	}
</style>
