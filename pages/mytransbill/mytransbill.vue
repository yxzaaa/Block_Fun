<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar 
			title="我的挂单" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full">
			<view class="fix-tabs-box">
				<view class="fix-tabs-item">
					<text :class="{active:activeTab == 1}" @click="toggleTab(1)">借款挂单</text>
				</view>
				<view class="fix-tabs-item">
					<text :class="{active:activeTab == 2}" @click="toggleTab(2)">投资挂单</text>
				</view>
			</view>
				<scroll-view scroll-y='true' style="width:100%;height:calc(100vh - 274upx);">
					<view style="padding:40upx;padding-bottom:0px;">
						<block v-for="(item,index) in borrowList" :key="index">
							<view class="debitbox">
								<view class="horizon-list-item">
									<text>{{getDate(item.created_on)}}</text>
									<text style="color:#DA53A2;">{{statusLib[item.status]}}</text>
								</view>
								<view class="debit-info">
									<view class="debit">
										<span class="text">USDT价格</span>
										<span class="number">{{item.price}}</span>
									</view>
									<view class="debit">
										<span class="text">抵押总量</span>
										<span class="number">{{getNum(item.amount)}}</span>
									</view>
									<view class="debit">
										<span class="text">放款总量</span>
										<span class="number">{{getNum(item.total)}}</span>
									</view>
									<view class="debit">
										<span class="text">周期(月)</span>
										<span class="number">
											{{item.month}}<span>月</span>
										</span>
									</view>
								</view>
								<view class="debit-btn">
									<text>{{getTimeDelay(item.expired_on)}}天后过期</text>
									<view>
										<view @click="billUpOrDown(item.id,item.status)">{{item.status == 2?'上架':'下架'}}</view>
									</view>
								</view>
							</view>
						</block>
					</view>
				</scroll-view>
			</view>
		</view>
	</view>
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	
	export default {
		components:{
			UniNavBar,
			UniBackground,
		},
		data() {
			return {
				scroll:0,
				activeTab:1,
				currpage:1,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},		
				},
				imageLib:{
					add:'../../static/icons/icon_add.png',
				},
				statusLib:{
					1:"已发布",
					2:"已下架",
					3:"已接单",
					4:"已完成",
					5:"已过期",
				},
				borrowList:[],
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
			this.updateList();
		},
		methods: {
			//获取我的挂单列表
			updateList(){
				uni.showLoading({
					title:'挂单加载中...'
				})
				this.$http({
					url:'/v1/main/debit/debit-my',
					data:{
						type:this.activeTab,
						page:this.currpage
					},
					success:res=>{
						console.log(res);
						if(res.code == 200){
							uni.hideLoading();
							this.borrowList = res.data.item;
						}
					}
				})
			},
			//挂单上下架
			billUpOrDown(id,status){
				if(status == 2){
					//挂单上架
					uni.showModal({
						title:'提示',
						content:'上架这条挂单？',
						confirmText:"上架",
						success:res=>{
							if(res.confirm){
								this.$http({
									url:'/v1/main/debit/debit-edit',
									data:{
										id,
										type:1
									},
									success:res=>{
										if(res.code == 200){
											uni.showToast({
												title:'挂单上架成功',
												icon:'none'
											})
											this.updateList();
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
				}else{
					//挂单下架
					uni.showModal({
						title:'提示',
						content:'下架这条挂单？',
						confirmText:"下架",
						success:res=>{
							if(res.confirm){
								this.$http({
									url:'/v1/main/debit/debit-edit',
									data:{
										id,
										type:2
									},
									success:res=>{
										if(res.code == 200){
											uni.showToast({
												title:'挂单已下架',
												icon:'none'
											})
											this.updateList();
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
			},
			getNum(num){
				return (parseFloat(num)).toFixed(2);
			},
			getDate(timestamp){
				var date = new Date(timestamp*1000);
				var year = date.getFullYear();
				var month = date.getMonth() + 1;
				var day = date.getDate();
				var hour = date.getHours();
				var min = date.getMinutes();
				month = month>=10?month:'0'+month;
				day = day>=10?day:'0'+day;
				hour = hour>=10?hour:'0'+hour;
				min = min>=10?min:'0'+min;
				return year+'/'+month+'/'+day+' '+hour+':'+min
			},
			getTimeDelay(end){
				var stamp = new Date().getTime();
				var overDay = parseInt((end*1000 - stamp)/(24*3600*1000));
				return overDay;
			},
			tabChange(value){
				this.activeTab = value.detail.current;
			},
			toggleTab(index){
				this.activeTab = index;
				this.updateList();
			},
			publish(){
				uni.navigateTo({
					url:'../publishborrow/publishborrow'
				})
			}
		}
	}
</script>

<style lang="scss" scoped> 
	.swiper-box{
		height:calc(100vh - 274upx);
	}
	.debitbox{
		width:670upx;
		background: rgba(45, 31, 37,0.8);
		border-radius: 8upx;
		margin-bottom:30upx;
		.horizon-list-item{
			padding:40upx;
			padding-bottom: 0;
			display: flex;
			justify-content: space-between;
			text{
				color:#999;
				font-size: 24upx;
			}
		}
		.debit-info{
			width:100%;
			padding:40upx;
			display: flex;
			justify-content: space-between;
			border-bottom:1px solid rgba(255,255,255,0.1);
			.debit{
				display: flex;
				flex-direction: column;
				justify-content: space-between;
				text-align:center;
				.text{
					font-size: 24upx;				
					color: #FFFFFF;					
					opacity: 0.5;
					span{
						font-size: 24upx;					
						color: #FFFFFF;
						margin-left:12upx;
					}
				}
				.number{
					margin-top:14upx;
					font-family: 'Montserrat-Bold';
					font-style: normal;
					font-weight: 600;
					font-size: 40upx;
					color: #FFFFFF;
					span{
						font-size: 22upx;					
						color: #FFFFFF;
						margin-left:8upx;
					}
				}
			}
		}
		.debit-btn{
			width:670upx;
			padding:30upx 40upx;
			display:flex;
			justify-content:space-between;
			align-items:center;
			text{
				color:#DA53A2;
				font-size: 24upx;
			}
			view{
				width:192upx;
				background: #DA53A2;
				border-radius: 200upx;
				text-align: center;
				line-height: 64upx;
				color: #FEFEFE;
				font-size: 28upx;
			}
			
		}
	}
	.fiexd-btn{
		position: fixed;
		right:70upx;
		bottom:120upx;
		background: #fff;
		width:98upx;
		height:96upx;
		border-radius: 48upx;
		box-shadow: 0px 0px 10px rgba(0, 9, 33, 0.4);
		display:flex;
		justify-content:center;
		align-items:center;
		z-index:998;
		image{
			width:64upx;
			height:64upx;
		}
	}
</style>
