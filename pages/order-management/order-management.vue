<template>
	<view class="container">
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="确认订单"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container fixbutton full">
			<!-- 新建收货地址 -->
			<navigator class="tosite" url="../choose-address/choose-address" v-if="hasDefault">
				<view class="site">
					<image src="../../static/bg/location.png" style="width:64upx;height:64upx;"></image>
					<span class="person-info">
						<span class="name-phone">
							<span class="name" style="font-size:28upx;color:#fff;">{{addressData.truename}}</span>
							<span class="phone" style="font-size:24upx;color:#999999;">{{addressData.mobile}}</span>
						</span>
						<span class="adress" style="font-size:24upx;display: block;color:#999999;width:500upx;">{{addressData.full}}</span>
					</span>
				</view>
				<image src="../../static/bg/right.png" style="width:40upx;height:40upx;"></image>
			</navigator>
			<navigator url="../address/addressManage" v-else>
				<view class="address">
					<view class="site">
						<image src="../../static/bg/location.png" style="width:64upx;height:64upx;"></image>
						<view class="toaddress" url="../address/addressManage">新建收货地址</view>
					</view>		
					<image src="../../static/bg/right.png" style="width:40upx;height:40upx;"></image>	
				</view>
			</navigator>
			<!-- 购物车详情 -->
			<view class="guess">
				<view class="guess-list">
					<view 
						v-for="(item, index) in guessList"
						:key="index"
						class="guess-item"	
					>
					<!-- 引入图片 -->
						<view class="image-wrapper">
							<image 
								:src="item.img" 
								mode="aspectFill"
								style="width:160upx;height:160upx;"
							></image>
						</view>
						<!-- 图片描述 -->
						<view class="guess-content" style="margin-left:20upx;margin-top:0;">
							<view style="font-size: 28upx;color:#fff;height:80upx;">{{item.title.length>36?item.title.substring(0,36)+' ...':item.title}}</view>
							<view style="font-size:24upx;color:#999999;margin-top:8upx;">消耗积分 {{item.credit*item.num}}</view>
							<view style="display: flex;justify-content: space-between;align-items: center;">
								<span style="color:#DA53A2;">
									<span style="font-size:24upx;display: inline-block;font-family:'Montserrat-Bold';">￥</span>
									<span style="display: inline-block;font-family:'Montserrat-Bold';">{{getPrice(item.price,item.num,0)}}.</span>
									<span style="font-size:24upx;display: inline-block;font-family:'Montserrat-Bold';">{{getPrice(item.price,item.num,1)}}</span>
								</span>
								<span class="cut" style="display: inline-block;color:rgba(255,255,255,0.5);font-size: 24upx;">
									数量：{{item.num}}
								</span>
							</view>
						</view>
					</view>
				</view>
			</view>
			<view class="fixed-buttons">
				<view class="button-group">
					<view class="finish">
						<view class="price">
							<span class="cash">
								<span style="font-size: 24upx;color:#999999">现金：</span>
								<span style="font-size: 24upx;color:#DA53A2;font-family:'Montserrat-Bold';">￥</span>
								<span style="font-size: 32upx;color:#DA53A2;font-family:'Montserrat-Bold';">{{String(totalCount.toFixed(4)).split('.')[0]}}.</span>
								<span style="font-size: 24upx;color:#DA53A2;font-family:'Montserrat-Bold';">{{String(totalCount.toFixed(4)).split('.')[1]}}</span>
							</span>
							<span>
								<span style="font-size: 24upx;color:#999999;">积分：</span>
								<span style="font-size: 24upx;color:#fff;">{{totalCredit}}</span>
							</span>
						</view>
						<fun-button @handle="submitOrder" value="提交订单" large wsssidth="240upx"></fun-button>
					</view>
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
				},
				hasDefault:false,
				addressData:{},
				guessList: [],
				totalCount:0,
				totalCredit:0,
				items:[],
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
			//获取当前订单信息
			this.items = uni.getStorageSync('skuCode');
			this.$http({
				url:'/mall/buy',
				type:'application/x-www-form-urlencoded',
				data:{
					item:JSON.stringify(this.items)
				},
				success:res=>{
					if(res.code == 200){
						if(res.data.address.length>0){
							this.hasDefault = true;
							this.addressData = res.data.address[0];
							this.addressData.full = res.data.address[0].address;
						}
						//设置订单商品信息
						this.guessList = [];
						res.data.mall.map(val=>{
							var username = val.username;
							val.item.map(val1=>{
								val1.username = username;
								this.guessList.push(val1);
							})
						})
						this.guessList.map(val=>{
							this.totalCount += parseFloat(val.price)*parseInt(val.num);
							this.totalCredit += parseInt(val.credit)*parseInt(val.num);
						})
						console.log(this.totalCount);
					}else{
						
					}
				}
			})
		},
		onShow(){
			if(uni.getStorageSync('currAddress')){
				uni.getStorage({
					key:'currAddress',
					success:res=>{
						console.log(res);
						this.hasDefault = true;
						this.addressData = res.data;
						uni.removeStorageSync('currAddress');
					}
				})
			}
		},
		methods:{
			//提交订单
			submitOrder(){
				if(this.addressData.truename){
					this.$http({
						url:'/mall/buy',
						type:'application/x-www-form-urlencoded',
						data:{
							item:JSON.stringify(this.items),
							truename:this.addressData.truename,
							address:this.addressData.full,
							mobile:this.addressData.mobile,
							submit:1
						},
						success:res=>{
							console.log(res);
							if(res.code == 200){
								uni.navigateTo({
									url:'../pay-order/pay-order?id='+res.data.id+'&amount='+res.data.amount
								})
							}else{
								uni.showToast({
									title:res.message,
									icon:'none'
								})
							}
						}
					})
				}else{
					uni.showToast({
						title:'请填写收货地址！',
						icon:'none'
					})
				}
			},
			getPrice(price,num,type){
				var totalPrice = parseFloat(price)*parseInt(num);
				totalPrice = totalPrice.toFixed(4);
				return totalPrice.split('.')[type];
			},
		}
		
	}
</script>

<style lang="scss" scoped>
	.tosite{
		width:750upx;
		height:140upx;
		padding:40upx;
		border-bottom:1px solid rgba(255,255,255,0.1);
		display:flex;
		align-items:center;
		justify-content:space-between;
		.tosite{
			display: flex;
		}
		.site{
			width:686upx;
			height:106upx;
			display: flex;
			align-items: center;
			.person-info{
				margin-left:20upx;
				.name-phone{
					display: flex;
					align-items: center;
				}
				.phone{
					margin-left:20upx;
				}
			}
			.toaddress{
				color:#fff;
				font-size:28upx;
				margin-left:32upx;
			}
		}
		
	}
	.address{
		width:750upx;
		padding:40upx;
		height:140upx;
		border-bottom:1px solid rgba(255,255,255,0.1);
		display:flex;
		align-items:center;
		justify-content:space-between;
		.site{
			display: flex;
			align-items: center;
			.toaddress{
				color:#fff;
				font-size:28upx;
				margin-left:16upx;
			}
		}
		
	}
	.guess {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items:center;
		padding:30upx 40upx 10upx;
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
			width:490upx;
			height:160upx;
			span,text{
				display: block;
			}
		}
	}
	.fixed-buttons{
		display: flex;
		justify-content: flex-end;
		align-items: center;
	}
	.button-group{
		width:500upx;
		display:flex;
		justify-content:flex-end;
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
					display: inline-block;
					line-height:32upx;
				}
			}
		}
	}
	
		
</style>
