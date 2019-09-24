<template>
	<view class="container">	
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="购物车"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
			@handle = "changeManage"
		/>
		<view class="app-container fixbutton full">
			<view class="guess">
				<view class="guess-list">
					<view class="guess-item" v-for="(item, index) in cartList" :key="index">
						<view style="line-height: 160upx;padding-right:40upx;display: flex;align-items: center;" @click="itemChoose(index)">
							<image
								:src="item.isActive?imageLib.checked:imageLib.check" 
								style="width:40upx;height:40upx;"
							></image>
						</view>
						<view class="image-wrapper">
							<image 
								:src="item.img" 
								mode="aspectFill"
								style="width:160upx;height:160upx;"
							></image>
						</view>
						<view class="guess-content" style="margin-left:20upx;margin-top:0;">
							<span style="font-size: 28upx;color:#fff;height:80upx;">{{item.title.length>36?item.title.substring(0,36)+' ...':item.title}}</span>
							<text style="font-size:24upx;color:#999999;margin-top:8upx;">消耗积分 {{item.credit*item.num}}</text>
							<span style="color:#DA53A2; position:relative;">
								<span style="font-size:24upx;margin-right:8upx;display: inline-block;font-family:'Montserrat-Bold';">￥</span>
								<span style="display: inline-block;font-family:'Montserrat-Bold';">{{getPrice(item.price,item.num,0)}}.</span>
								<span style="font-size:24upx;display: inline-block;font-family:'Montserrat-Bold';">{{getPrice(item.price,item.num,1)}}</span>
								<span class="cut" style="position:absolute;right:10upx;display: inline-block;bottom:8upx;">
									<span style="margin-right:20upx;font-size:30upx;color:#fff;font-weight: bold;display: inline-block;" @click="setNum(index,0)"> - </span>
									<span style="display:inline-block;#99999;background:#280617;font-size:24upx;color:#fff;width:64upx;height:40upx;line-height: 40upx;text-align: center;">{{item.num}}</span>
									<span style="margin-left:20upx;font-size:30upx;color:#fff;font-weight: bold;display: inline-block;" @click="setNum(index,1)"> + </span>
								</span>
							</span>
						</view>
					</view>
				</view>
			</view>
			
			<view class="fixed-buttons" style="z-index: 1000;" v-if="isManager">
				<view class="button-group">
					<view class="check" @click ="chooseAll">
						<image :src="isChooseAll?imageLib.checked:imageLib.check"></image>
						<span>全选</span>
					</view>
					<view class="finish">
						<view class="price">
							<span class="cash">
								<span style="font-size: 24upx;color:#999999">现金：</span>
								<span style="font-size: 24upx;color:#DA53A2;font-family:'Montserrat-Bold';">￥</span>
								<span style="font-size: 28upx;color:#DA53A2;font-family:'Montserrat-Bold';">{{String(totalCount.toFixed(4)).split('.')[0]}}.</span>
								<span style="font-size: 24upx;color:#DA53A2;font-family:'Montserrat-Bold';">{{String(totalCount.toFixed(4)).split('.')[1]}}</span>
							</span>
							<span>
								<span style="font-size: 24upx;color:#999999;">积分：</span>
								<span style="font-size: 24upx;color:#fff;">{{String(totalCredit)}}</span>
							</span>
						</view>
						<fun-button value="去结算" large width="240upx" @handle="goOrderPage"></fun-button>
					</view>
				</view>
			</view>
			
			<view class="fixed-buttons">
				<view class="button-group">
					<view class="check" @click = "chooseAll">
						<image :src="isChooseAll?imageLib.checked:imageLib.check"></image>
						<span>全选</span>
					</view>
					<fun-button value="删除" width="240upx" large @handle="deleteCart"></fun-button>
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
						text:"管理",
						type:'handle',
					},
					
				},
				imageLib:{
					checked:'../../static/bg/check.png',
					check:'../../static/bg/checkbox.png',
				},
				isManager:true,
				isChooseAll:false,
				cartList:[
				],
				totalCount:0,
				totalCredit:0,
				
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
			this.updateList();
		},
		methods:{
			updateList(){
				uni.showLoading({
					title:'购物车加载中...'
				})
				this.$http({
					url:'/mall/cart',
					success:res=>{
						console.log(res);
						if(res.code == 200){
							uni.hideLoading();
							if(res.data[0]){
								this.cartList = [];
								res.data.map(val=>{
									var username = val.username;
									val.item.map(val1=>{
										val1.username = username;
										this.cartList.push(val1);
									})
								})
								this.cartList.map(item=>{
									item.isActive = false;
								});
							}else{
								this.cartList = [];
							}
						}
					}
				})
			},
			getPrice(price,num,type){
				var totalPrice = parseFloat(price)*parseInt(num);
				totalPrice = totalPrice.toFixed(4);
				return totalPrice.split('.')[type];
			},
			setNum(index,type){
				if(type == 0){
					if(this.cartList[index].num > 1){
						this.cartList[index].num --;
					}
				}else if(type == 1){
					if(this.cartList[index].num < this.cartList[index].amount){
						this.cartList[index].num++;
					}else{
						uni.showToast({
							title:'数量已达库存上限',
							icon:'none'
						})
					}
				}
				this.totalCount = 0;
				this.totalCredit = 0;
				this.cartList.map(val=>{
					if(val.isActive){
						this.totalCount += parseFloat(val.price)*parseInt(val.num);
						this.totalCredit += parseInt(val.credit)*parseInt(val.num);
					}
				})
			},
			goOrderPage(){
				var skuInfo = [];
				this.cartList.map(val=>{
					if(val.isActive ==true){
						var codeObj = {};
						codeObj[val.code] = val.num;
						skuInfo.push(codeObj);
					}
				})
				if(skuInfo.length>0){
					uni.setStorage({
						key:'skuCode',
						data:skuInfo,
						success:()=>{
							//立即购买
							uni.navigateTo({
								url: '../order-management/order-management',
							});
						}
					})
				}else{
					uni.showToast({
						title:'请选择结算商品',
						icon:'none'
					})
				}
			},
			changeManage(){
				if(this.isManager){
					this.isManager = false;
					this.navButtons.textbtn = {
						text:'完成',
						type:'handle',
					}
				}else{
					this.isManager = true;
					this.navButtons.textbtn = {
						text:'管理',
						type:'handle',
					}
				}
			},
			itemChoose(index){
				if(this.cartList[index].isActive){
					// this.cartList[index].isActive = false; //方法一
					this.$set(this.cartList[index],'isActive',false); //方法二
				}else{
					// this.cartList[index].isActive = true;
					this.$set(this.cartList[index],'isActive',true);
				}
				var isAll = true;
				this.cartList.map(item=>{
					if(item.isActive == false){
						isAll = false;
						return;
					}
				});
				this.isChooseAll = isAll;
				
				this.totalCount = 0;
				this.totalCredit = 0;
				this.cartList.map(val=>{
					if(val.isActive){
						this.totalCount += parseFloat(val.price)*parseInt(val.num);
						this.totalCredit += parseInt(val.credit)*parseInt(val.num);
					}
				})
			},
			chooseAll(){
				if(this.isChooseAll){
					this.isChooseAll = false;
					this.cartList.map(item=>{
						item.isActive = false;
					})
				}else{
					this.isChooseAll = true;
					this.cartList.map(item=>{
						item.isActive = true;
					})
				}
				
				this.totalCount = 0;
				this.totalCredit = 0;
				this.cartList.map(val=>{
					if(val.isActive){
						this.totalCount += parseFloat(val.price)*parseInt(val.num);
						this.totalCredit += parseInt(val.credit)*parseInt(val.num);
					}
				})
			},
			deleteCart(){
				console.log(this.cartList);
				var codes = [];
				this.cartList.map(item=>{
					if(item.isActive){
						codes.push(item.code);
					}
				})
				console.log(codes.join(','));
				this.$http({
					url:'/mall/cart',
					type:'application/x-www-form-urlencoded',
					data:{
						action:'delete',
						code:codes.join(',')
					},
					success:res=>{
						console.log(res);
						if(res.code == 200){
							this.updateList();
						}
					}
				})
			}
		}
		
	}
</script>

<style lang="scss" scoped>
	
	.guess {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items:center;
		padding:0upx 40upx 10upx;
	}
	.guess-list {
		margin:0 auto;
		// display: flex;
		// flex-wrap: wrap;
		width:670upx;
	}
	.guess-item {
		display: flex;
		width:100%;
		padding-bottom: 40upx;
	
		.image-wrapper{
			width: 160upx;
			height: 160upx;
			border-radius: 8upx;
			overflow: hidden;
		}
		.guess-content{
			height:160upx;
			width:420upx;
			span,text{
				display: block;
			}
		}
	}
	.fixed-buttons{
		
	}
	.button-group{
		width:670upx;
		display:flex;
		justify-content:space-between;
		.check{
			display:flex;
			align-items:center;
			image{
				margin-right:16upx;
				width:32upx;
				height:32upx;
			}
			span{
				color: #999999;
				font-size: 24upx;
			}
		}
		.finish{
			display: flex;
			align-items: center;
			.price{
				display: flex;
				margin-right:20upx;
				flex-direction: column;
				align-content: center;
				align-items: flex-end;
				span{
					line-height:32upx;
					display: inline-block;
				}
			}
		}
	}
		
</style>
