<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar
			title="编辑收货地址"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
			@handle="deleteAddress"
		/>
		<view class="app-container full">
			<view class="content" style="padding:40upx;">
				<view class="row b-b">
					<text class="tit" style="padding-top:0px;">收货人姓名</text>
					<input class="input" type="text" v-model="getterName" placeholder="请输入收货人姓名" placeholder-style="color:rgba(255,255,255,0.5)"/>
				</view>
				<view class="row b-b">
					<text class="tit">手机号</text>
					<input v-model="phone" class="input" type="number" placeholder="请输入11位手机号" placeholder-style="color:rgba(255,255,255,0.5)"/>
				</view>
				<view class="row b-b">
					<text class="tit">所属区域</text>
					<picker mode="multiSelector" :range="rangeData" :range-key="'name'" @columnchange="setAddressData" @change="changeArea" :disabled="loadingMPData"
						style="position:relative;"
					>
						<input v-model="area" class="input" type="text" :placeholder="loadingMPData?'正在加载省市区信息...':'请选择省市区'" disabled placeholder-style="color:rgba(255,255,255,0.5)">
						<image :src="imageLib.shape" style="width:24upx;height:12upx;position: absolute;top:34upx;right:10upx;"></image>
					</picker>
				</view>
				<view class="row b-b"> 
					<text class="tit">详细地址</text>
					<input v-model="address" class="input" type="text" placeholder="请输入详细地址" placeholder-style="color:rgba(255,255,255,0.5)"/>
				</view>
				
			</view>
			<view class="default" style="padding:30upx 40upx;display: flex;align-items: center;" @click="isdefault = isdefault?false:true">
				<image :src="isdefault?imageLib.check:imageLib.checkbox" style="width:40upx;height:40upx;margin-right:14upx;"></image>
				<text style="color:#fff;font-size: 24upx;">设为默认</text>
			</view>
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button @handle="addressPlus" value="保存" width="670upx"  large></fun-button>
				</view>
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
					},
					textbtn:{
						type:'normal',
						text:'删除',
						type:'handle'
					}
				},
				imageLib:{
					check:'../../static/bg/check.png',
					checkbox:'../../static/bg/checkbox.png',
					shape:'../../static/icons/Shape1.png',
				},
				addressid:null,
				getterName:'',
				phone:'',
				area:'',
				areaid:null,
				address:'',
				isdefault:false,
				rangeData:[],
				addressData:[],
				loadingMPData:true,
				province:new Set(),
				citys:new Set(),
				areas:new Set()
			}
		},
		onPageScroll(val){
			this.scroll=val.scrollTop
		},
		onLoad(){
			//获取当前编辑的收货地址数据
			uni.getStorage({
				key:'currEditAddress',
				success:res=>{
					console.log(res);
					this.getterName = res.data.truename;
					this.phone = res.data.mobile.slice(2);
					this.address = res.data.address;
					this.addressid = res.data.id;
				}
			})
			//收货地址数据
			this.$http({
				url:'/file/static/area.json',
				method:'GET',
				success:res=>{
					this.addressData = new Set(res);
					this.addressData.forEach((element)=>{
					    if(element.parentid == 0){
							this.province.add(element);
						}
					});
					var provinceID = Array.from(this.province)[0].areaid;
					this.addressData.forEach((element)=>{
					    if(element.parentid == provinceID){
							this.citys.add(element);
						}
					});
					var cityID = Array.from(this.citys)[0].areaid;
					this.addressData.forEach((element)=>{
					    if(element.parentid == cityID){
							this.areas.add(element);
						}
					});
					this.rangeData = [Array.from(this.province),Array.from(this.citys),Array.from(this.areas)];
					this.loadingMPData = false;
				}
			})
		},
		methods: {
			//切换省市区
			changeArea(e){
				var values = e.detail.value;
				values[1] = values[1] === undefined?0:values[1];
				values[2] = values[2] === undefined?0:values[2];
				this.area = Array.from(this.province)[values[0]].name + Array.from(this.citys)[values[1]].name;
				this.areaid = Array.from(this.citys)[values[1]].areaid;
				if(Array.from(this.areas)[values[2]]){
					this.area += Array.from(this.areas)[values[2]].name;
					this.areaid = Array.from(this.areas)[values[2]].areaid;
				}
			},
			//设置省市区数据
			setAddressData(e){
				var column = e.detail.column;
				var value = e.detail.value;
				if(column == 0){
					this.citys.clear();
					this.areas.clear();
					var provinceID = Array.from(this.province)[value].areaid;
					this.addressData.forEach((element)=>{
					    if(element.parentid == provinceID){
							this.citys.add(element);
						}
					});
					var cityID = Array.from(this.citys)[0].areaid;
					this.addressData.forEach((element)=>{
					    if(element.parentid == cityID){
							this.areas.add(element);
						}
					});
					this.rangeData = [Array.from(this.province),Array.from(this.citys),Array.from(this.areas)];
				}else if(column == 1){
					this.areas.clear();
					var cityID = Array.from(this.citys)[value].areaid;
					this.addressData.forEach((element)=>{
					    if(element.parentid == cityID){
							this.areas.add(element);
						}
					});
					this.rangeData = [Array.from(this.province),Array.from(this.citys),Array.from(this.areas)];
				}
			},
			//修改收货地址
			addressPlus(){
				this.$http({
					url:'/member/address',
					data:{
						action:'edit',
						areaid:this.areaid,
						truename:this.getterName,
						mobile:'86'+this.phone,
						address:this.address,
						default:this.isdefault?1:0,
						id:this.addressid
					},
					type:'application/x-www-form-urlencoded',
					success:res=>{
						console.log(res);
						if(res.code == 200){
							uni.navigateBack({
								delta:1
							})
						}else{
							uni.showToast({
								title:res.message,
								icon:'none'
							})
						}
					}
				})
			},
			//删除收货地址
			deleteAddress(){
				uni.showModal({
					title:'删除收货地址',
					content:'您要删除这条收货地址吗？',
					success:res=>{
						if(res.confirm){
							this.$http({
								url:'/member/address',
								data:{
									action:'delete',
									id:this.addressid
								},
								type:'application/x-www-form-urlencoded',
								success:res=>{
									console.log(res);
									if(res.code == 200){
										uni.navigateBack({
											delta:1
										})
									}else{
										uni.showToast({
											title:res.message,
											icon:'none'
										})
									}
								}
							})
						}
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.content{
		margin: 0upx 40upx 0;
		border-radius:10upx;
		background: rgba(45, 31, 37, 0.7);
	}

	.row{
		display: flex;
		flex-direction: column;
		align-content: space-around;
		width:590upx;
		
		
		.tit{
			font-size: 28upx;
			color: #fff;
			padding-top:40upx;
			padding-bottom:10upx;
			display: block;
		}
		.input{
			flex: 1;
			font-size: 24upx;
			height:80upx;
			color: rgba(255,255,255,0.7);
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
